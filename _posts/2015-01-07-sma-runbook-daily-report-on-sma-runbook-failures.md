---
layout: post
title: SMA Runbook Daily Report On SMA Runbook Failures
date: 2015-01-07 02:15
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, PowerShell, powershell, SMA, sma]
---
The sad reality of using Service Management Automation is that it can be a little iffy in the stability department. That being so, I decided to put together an SMA runbook that would report on all the other SMA runbook failures of the last 24 hours. Yes, I realize the irony in using SMA to report on its own runbook failures. One must have faith in one's infrastructure and this particular runbook.

First things first, I need to declare my runbook/workflow and get the stored variable asset which holds my SMTP server.

```
workflow GetDailyFailedJobs
{
    $smtpserver = Get-AutomationVariable -Name 'SMTPServer'
}
```

Easy! Now the SMA PowerShell cmdlets work best in actual PowerShell, not in workflows so I'm going to cheat and use an inlinescript block to hold pretty much everything else. Now before we get to the good stuff, I'm going to knock out the easy task of setting up my try and catch blocks as well as my function that sends email.

```
workflow GetDailyFailedJobs
{
    $smtpserver = Get-AutomationVariable -Name 'SMTPServer'
    InlineScript
    {
        Try
        {
            $smtpServer = $using:smtpServer
            $smtpSubject = "SMA Job Failure List"
            $body = "Better put something in here!"
            $emailaddress = @("thmsrynr@outlook.com","someone@else.com")
            send-mailmessage -to $emailaddress -From "SMA_MGMT@else.com" -Subject $smtpSubject -SMTPServer $smtpserver -body $body -bodyashtml
        }
        Catch [Exception]
        {
            $smtpServer = Get-AutomationVariable -Name 'ABC-SMTPServer'
            $smtpSubject = "FAILURE: GetFailedJobs failed"
            $body = "GetFailedJobs failed"
            $emailaddress = @("thmsrynr@outlook.com","someone@else.com")
            send-mailmessage -to $emailaddress -From "SMA_MGMT@else.com" -Subject $smtpSubject -SMTPServer $smtpserver -body $body -bodyashtml
        }
    }
}
```

Most of this is pretty straight forward. I'm going to put some stuff in a try block and email it out if it works. If I catch an error, I'm going to email a notification that something screwed up in the try block.

Now the meat and potatoes. Something actually worth making a blog entry for! We need to build the content of the email we're sending in the try block. Right now it's just text that says "better put something in here" and it's right. We better.

```
workflow GetDailyFailedJobs
{
    $smtpserver = Get-AutomationVariable -Name 'SMTPServer'
    InlineScript
    {
        Try
        {
            $arrFailedJobs = Get-SMAJob -Webserviceendpoint "https://sma-mgmt-server.else.com" | Where-Object -Property JobException | Where-object -Property endtime -gt ((get-Date).AddMinutes(-1440)).ToUniversalTime()
            If($arrFailedJobs)
            {
                $strHtmlMail = '&lt;html&gt;&lt;body&gt;&lt;table style="padding: 6px; border: 1px solid #000000; border-collapse: collapse;"&gt;&lt;tr style="background-color: #6388FF;  color: #FFFFFF;"&gt;&lt;td&gt;RunbookName&lt;/td&gt;&lt;td&gt;Start Time&lt;/td&gt;&lt;td&gt;End Time&lt;/td&gt;&lt;td&gt;Error&lt;/td&gt;&lt;/tr&gt;' 
                ForEach($objFailedJob in $arrFailedJobs)
                {
                    $strFailedJobStart = $objFailedJob.StartTime
                    $strFailedJobEnd =$objFailedJob.EndTime
                    $objFailedRunbook = Get-SmaRunbook -WebServiceEndPoint "https://sma-mgmt-01.abcp.ab.bluecross.ca" -ID $objFailedJob.RunbookId
                    $strFailedRunbook = $objFailedRunbook.RunbookName
                    $strFailedJobError = $objFailedJob.JobException
                    $strHtmlMail += '&lt;tr style="background-color: #B27272;  color: #FFFFFF;"&gt;&lt;td style="border:1px solid #000000"&gt;' + ${strFailedRunbook} + '&lt;/td&gt;&lt;td style="border:1px solid #000000"&gt;' + ${strFailedJobStart} + '&lt;/td&gt;&lt;td style="border:1px solid #000000"&gt;' + ${strFailedJobEnd} + '&lt;/td&gt;&lt;td style="border:1px solid #000000"&gt;' + ${strFailedJobError} + '&lt;/td&gt;&lt;/tr&gt;'
                }
                $strHtmlMail += "&lt;/table&gt;&lt;/body&gt;&lt;/html&gt;"
                
                $smtpServer = $using:smtpServer
                $smtpSubject = "SMA Job Failure List"
                $body = $strHtmlMail
                $emailaddress = @("thmsrynr@outlook.com","someone@else.com")
                send-mailmessage -to $emailaddress -From "SMA_MGMT@else.com" -Subject $smtpSubject -SMTPServer $smtpserver -body $body -bodyashtml
            }
        }
        Catch [Exception]
        {
            $smtpServer = Get-AutomationVariable -Name 'ABC-SMTPServer'
            $smtpSubject = "FAILURE: GetFailedJobs failed"
            $body = "GetFailedJobs failed"
            $emailaddress = @("thmsrynr@outlook.com","someone@else.com")
            send-mailmessage -to $emailaddress -From "SMA_MGMT@else.com" -Subject $smtpSubject -SMTPServer $smtpserver -body $body -bodyashtml
        }
    }
}
```

Wow that got a little ugly really quickly. What you need to keep in mind is that a lot of this ugliness is styling to make the email report pretty. That's a little counter-intuitive but, hey, welcome to scripting as a working sysadmin. Let's break it down line by line.

Line 8 is getting an array of failed jobs in the last day. It's a big pipeline which:

<ul>
    <li>Gets the jobs</li>
    <li>Where there's a JobException property on the job</li>
    <li>Where the endtime is greater than within the last day</li>
</ul>

In Line 9 t0 20, if there are jobs in the array of failed jobs within the last day, we have to build a report. Line 11 initializes the HTML that will become the body of our report by putting in a table, its column headers and styling it.

Starting on Line 12, for each failed job in the array of failed jobs, we're adding a row to our HTML table with the start time, end time, the runbook ID, the runbook name and the exception that was thrown.

On lines 19 to 21 we finish off our HTML for the body of our email. Then we use the code we already wrote to send it to us.

Boom. Pretty nice report on failed jobs. Hopefully you never see one in your inbox, otherwise you're going to have some troubleshooting to do.
