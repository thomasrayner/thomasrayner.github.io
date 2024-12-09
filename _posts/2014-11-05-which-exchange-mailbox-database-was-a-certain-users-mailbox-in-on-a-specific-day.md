---
layout: post
title: Which Exchange Mailbox Database Was A Certain User's Mailbox In On A Specific Day?
date: 2014-11-05 09:00
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, Exchange, exchange, PowerShell, powershell, SMA, sma]
---
In Exchange, user mailboxes are stored in databases. You regularly back up these databases, don't you? Good.

Now imagine the following. User A has a mailbox in Database01. This database is backed up daily. Now imagine User A's mailbox was moved to another database, Database02. What if User A came to you and needed something recovered? Okay no problem, load up the backup for Database02 and you can recover anything for that user since the user has been on Database02. Wait, what do you mean you want something from BEFORE you were on your current database, User A? How am I supposed to know what database backup I need to mount to find your stuff? Exchange only knows what database you're on, not what database you came from! Your data is on a backup for who knows which database!

My solution for this is a bit bulky. It involves automating a script to export a list of all users and the database they're on. The idea is, if you export this list daily, you will have an archive of what database all your users are on for any given day. Even if they move, you can reference the output from this script and see which database their mailbox was on during the day in question. Then you will know which database's backup you need to load to help User A get his stuff back.

For automation, I am using <a title="SMA" href="http://technet.microsoft.com/en-us/library/dn469260.aspx" target="_blank">Service Management Automation</a> (SMA). I love SMA. It uses PowerShell Workflows which are kinda, sorta, almost like regular ol' PowerShell with some differences. I'll point out the parts of my solution that aren't vanilla PowerShell.

First things first, I need to declare my workflow and stick a Try Catch block in it:

```
workflow ExchangeMailboxDBList
{
    try
    {

    }
    catch [Exception]
    {
        $emailaddress = "ThmsRynr@outlook.com"
        $smtpSubject = "Exchange List Failure"
        $smtpserver = Get-AutomationVariable -Name 'SMTPServer'
        $body = "Could not connect to my server"
        send-mailmessage -to $emailaddress -From "your_service_account@domain.com" -Subject $smtpSubject -SMTPServer $smtpserver -body $body
    }
}
```

We're already running into something funny. What is <strong>Get-AutomationVariable -Name 'SMTPServer'</strong>? In SMA, you can store variables for any of your runbooks to use. This cmdlet is retrieving the previously stored value for my SMTP server. This is nice because if I change SMTP servers, I can update the single SMA asset instead of updating all my scripts individually.

Great! Now let's actually write the part of the script that does something useful. Let's start by initializing some variables:

```
workflow ExchangeMailboxDBList
{
    try
    {
       $mailboxes = inlinescript{ 
        $connectionURI = "http://fqdn.to.your.server/Powershell"
        $getMBXconn = new-pssession -configurationname Microsoft.Exchange -connectionuri $connectionURI -authentication kerberos
       }
    }
    catch [Exception]
    {
        $emailaddress = "ThmsRynr@outlook.com"
        $smtpSubject = "Exchange List Failure"
        $smtpserver = Get-AutomationVariable -Name 'SMTPServer'
        $body = "Could not connect to my server"
        send-mailmessage -to $emailaddress -From "your_service_account@domain.com" -Subject $smtpSubject -SMTPServer $smtpserver -body $body
    }
}
```

A couple new lines in the Try block! $connectionURI is pretty straight forward. You're going to make a remote session to the Exchange Management Shell on your Exchange Server so your script needs to know where that is. $getMBXconn is a new PSSession to the URI you specified. Notice that I'm not passing any credentials specifically to this one. The service account that's running this SMA runbook has the rights it needs to do this. You can either do the same or you can pass specific credentials from an SMA asset or stored elsewhere.

What is it all wrapped in, though? Some inlinescript block? Like I mentioned above, PowerShell Workflows are different than PowerShell. Some of the commands coming up don't work in PowerShell Workflows but do work in PowerShell. By wrapping the PowerShell script in an inlinescript block, it executes like real PowerShell instead of a PowerShell Workflow. The outcome of this inlinescript is going to get assigned to $mailboxes.

We have our connection, now we need to actually go get some data:

```
workflow ExchangeMailboxDBList
{
    try
    {
       $mailboxes = inlinescript{ 
        $connectionURI = "http://fqdn.to.your.server/Powershell"
        $getMBXconn = new-pssession -configurationname Microsoft.Exchange -connectionuri $connectionURI -authentication kerberos

    try
    {
        $mbx = invoke-command {
         get-mailbox -resultsize unlimited -erroraction silentlycontinue | Select-Object -property database, name, ServerName, Guid 
         } -session $getMBXconn
         $mbx
     }

     catch [Exception]
     {
     $emailaddress = "ThmsRynr@outlook.com"
     $smtpSubject = "Exchange List Failure"
     $smtpserver = Get-AutomationVariable -Name 'SMTPServer'
     $body = "Could not invoke command on server"
     send-mailmessage -to $emailaddress -From "your_service_account@domain.com" -Subject $smtpSubject -SMTPServer $smtpserver -body $body
     }

     remove-pssession $getMBXconn
    }

    $sOut = Get-AutomationVariable -Name 'ABC-OUTFOLDER'
    $mailboxes | Sort-object -property database, name | Export-Csv -Path "$sOut\ExchangeBackups\MBX_Tracking$(get-date -f yyyy-MM-dd_HH_mm).csv" -NoTypeInformation
    }
    catch [Exception]
    {
        $emailaddress = "ThmsRynr@outlook.com"
        $smtpSubject = "Exchange List Failure"
        $smtpserver = Get-AutomationVariable -Name 'SMTPServer'
        $body = "Could not connect to my server"
        send-mailmessage -to $emailaddress -From "your_service_account@domain.com" -Subject $smtpSubject -SMTPServer $smtpserver -body $body
    }
}
```

Alright that looks like a lot of stuff at once, but it wasn't actually too crazy. Let's break down what we added.

Lines 17 - 24 are just another Catch block to tell us if we messed up in lines 11 - 13.

On lines 11 - 13, we're invoking a command in our remote session. We're running a get-mailbox, specifying that we want all of them and that we don't want to stop on an error. We pipe that into a select-object command to filter out only data we want, the database, name of the mailbox, the server the database is on and the guid. On line 13, we write that data (which in turn is assigned to $mailboxes since $mailboxes is the value of whatever comes out of the inlinescript).

On line 26, we get rid of our PSSession.

On lines 29 and 30 we're writing our findings to a csv file and naming it in a way that includes the current date and time. That's how we know what script output is for which day.

That's our final solution! All you need to do now is create the SMA schedule to run this as frequently as it makes sense for you. You might also want to include some logic to clean up old files. Then you can just go to the output folder, find the file that corresponds with the day you care about and find the database that User A was on the day they deleted the wrong file.
