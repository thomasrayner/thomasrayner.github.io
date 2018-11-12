---
layout: post
title: Getting Your Organizations Largest Exchange Mailboxes With PowerShell
date: 2016-01-27 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, Exchange, exchange, microsoft, PowerShell, powershell, PowerShell ISE, powershell ise, remote admin]
---
In a quest to hunt down users with large mailboxes, I wrote the following PowerShell function. It's made to be run from a <a href="http://www.workingsysadmin.com/opening-a-remote-exchange-management-shell/" target="_blank">Remote Exchange Management Shell connection</a> instead of by logging into an Exchange server via remote desktop and running such a shell manually. Remote administration is the future!

My requirements were rather basic. I wanted a function that would return the top 25 (or another number of my choosing) Exchange mailboxes in my organization by total size. I also wanted the ability to specify an individual user's mailbox to see how large the specific box is.

So, let's get started.

```
function Get-LargeMailbox
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $False)]
        [int]$Top = 1,
        [Parameter(Mandatory = $False,
                Position = 1,
        ValueFromPipeline = $True)]
        [string]$Identity = '*'
    )
}
```

All I've done here is declare my new function named <strong>Get-LargeMailbox </strong>and specified its parameters. $Top is the integer representing the number of mailboxes to return (defaulted to 1) and $Identity is the specific mailbox we want to return (defaulted to * which will return all mailboxes).

Now, I know I need to get my mailboxes and retrieve some statistics.

```
function Get-LargeMailbox
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $False)]
        [int]$Top = 1,
        [Parameter(Mandatory = $False,
                Position = 1,
        ValueFromPipeline = $True)]
        [string]$Identity = '*'
    )
        
    Get-Mailbox -Identity $Identity -ResultSize Unlimited |
    Get-MailboxStatistics 
}
```

So far, so good. We haven't narrowed down the stats we care about yet but we're getting all the mailboxes in the organization and retrieving all the stats for them. Now we're about to run into a problem. There's a property returned by <strong>Get-MailboxStatistics</strong> called TotalItemSize but when you're in a remote session, but, it's hard to work with. Observe.

```
PS C:\&gt; (Get-Mailbox ThmsRynr | Get-MailboxStatistics).TotalItemSize | Format-List


IsUnlimited : False
Value       : 2.303 GB (2,473,094,022 bytes)
```

You can see it returns a property consisting of a boolean value for if my quota is unlimited, and then a value of what my total size is. Ok, so that value is probably a number, right?

```
PS C:\&gt; (Get-Mailbox ThmsRynr| Get-MailboxStatistics).TotalItemSize.Value | Get-Member


   TypeName: Deserialized.Microsoft.Exchange.Data.ByteQuantifiedSize
#output omitted
```

Well, yeah, it is. The Value of TotalItemSize is a number but it's a <em>Deserialized.Microsoft.Exchange.Data.ByteQuantifiedSize </em>and when you're connected to a remote Exchange Management Shell, you don't have that library loaded unless you install some tools on your workstation. Rather than do that, can't we just fool around with it a bit and avoid installing a bunch of superfluous Exchange management tools? I bet we can, especially since this value has a ToString() method associated with it.

Back to our function. I need to sort the results of my "Get all the mailboxes, get all their stats" command by the total size of the mailboxes.

```
function Get-LargeMailbox
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $False)]
        [int]$Top = 1,
        [Parameter(Mandatory = $False,
                Position = 1,
        ValueFromPipeline = $True)]
        [string]$Identity = '*'
    )
        
    Get-Mailbox -Identity $Identity -ResultSize Unlimited |
    Get-MailboxStatistics |
    Sort-Object -Property @{
        e = {
            $_.TotalItemSize.Value.ToString().split('(').split(' ')[-2].replace(',', '') -as [double]
        }
    } -Descending 
}
```

Oh boy, string manipulation is always fun, isn't it? What I've done here is sorted my mailboxes by an expression. That expression is the result of converting the value of the TotalItemSize attribute to a string and manipulating it. I'm splitting it on the open bracket character, and then again on the space character. I'm taking the second last item in that array, stripping out the commas and casting it as a double (because some values are too big to be integers). That's a lot of weird string manipulation for some of you to get your heads around, but look at the string returned by default. I need the number of bytes and that was the best way to get it.

Now all I need to do is select the properties from my sorted list of mailboxes and return the top number of results. Here's the final function.

```
function Get-LargeMailbox
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $False)]
        [int]$Top = 1,
        [Parameter(Mandatory = $False,
                Position = 1,
        ValueFromPipeline = $True)]
        [string]$Identity = '*'
    )
        
    Get-Mailbox -Identity $Identity -ResultSize Unlimited |
    Get-MailboxStatistics |
    Sort-Object -Property @{
        e = {
            $_.TotalItemSize.Value.ToString().split('(').split(' ')[-2].replace(',', '') -as [double]
        }
    } -Descending |
    Select-Object -Property DisplayName, @{
        l = 'MailboxSize'
        e = {
            $_.TotalItemSize.Value.ToString().split('(').split(' ')[-2].replace(',', '') -as [double]
        }
    } -First $Top
}
```

Now you can do things like this.

```
#See how big my individual mailbox is
Get-LargeMailbox -Identity ThmsRynr

#Get the largest 20 mailboxes in the organization
Get-LargeMailbox -Top 20

#Get the mailboxes for a specific AD group and sort by size
$arrLargeMailboxes = @()
(Get-ADGroupMember 'GroupName' -Recursive).SamAccountName | ForEach-Object -Process {
    $arrLargeMailboxes += Get-LargeMailbox -Identity $_ 
}
$arrLargeMailboxes |
Sort-Object -Property MailboxSize -Descending |
Select-Object -Property DisplayName, @{
    l = 'MailboxSize'
    e = {
        '{0:N0}' -f $_.MailboxSize
    }
} |
Format-Table -AutoSize
```

Before we end, let's take a closer look at the last example.

First, I'm declaring an array to hold the results of users and how large their mailbox is. Then I'm getting all the members of a group, taking the SamAccountName and performing an action on each of them. That action, of course, is retrieving their mailbox size using the function I just wrote and appending the results to the array. Then I need to sort that array and display it. The <strong>Select-Object</strong> command has the formatting I included to make the mailbox sizes have commas separating every three digits.
