---
layout: post
title: Getting Large Exchange Mailbox Folders With PowerShell
date: 2016-02-17 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, Exchange, exchange, PowerShell, powershell, PowerShell ISE, powershell ise, storage]
---
I've been continuing my quest to identify users who have large Exchange mailboxes.<a href="http://www.workingsysadmin.com/getting-your-organizations-largest-exchange-mailboxes-with-powershell/" target="_blank"> I wrote a function in my last post to find large Exchange mailboxes</a>, but, I wanted to take this a step further and identify the large folders within user mailboxes that could stand to be cleaned out. For instance, maybe I want to find all the users who have a large Deleted Items folder or Sent Items or Calendar. You get the idea. It’s made to be run from a <a href="http://www.workingsysadmin.com/opening-a-remote-exchange-management-shell/" target="_blank">Remote Exchange Management Shell connection</a> instead of by logging into an Exchange server via remote desktop and running such a shell manually. Remote administration is the future (just like my last post)!

So, let's define the function and parameters.

```
function Get-LargeFolder 
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $False)]
        [ValidateSet('All', 'Calendar', 'Contacts', 'ConversationHistory', 'DeletedItems', 'Drafts', 'Inbox', 'JunkEmail', 'Journal', 'LegacyArchiveJournals', 'ManagedCustomFolder', 'NonIpmRoot', 'Notes', 'Outbox', 'Personal', 'RecoverableItems', 'RssSubscriptions', 'SentItems', 'SyncIssues', 'Tasks')]
        [string]$FolderScope = 'All',
        [Parameter(Mandatory = $False)]
        [int]$Top = 1,
        [Parameter(Mandatory = $False,
                Position = 1,
        ValueFromPipeline = $True)]
        [string]$Identity = '*'
    )
}
```

My function is going to be named <strong>Get-LargeFolder</strong> and takes three parameters. $FolderScope is used in the <strong>Get-MailboxFolderStatistics</strong> cmdlet (spoiler alert) and must belong to the set of values specified. $Top is an integer used to define how many results we're going to return and $Identity can be specified as an individual username to examine a specific mailbox, or left blank (defaulted to *) to examine the entire organization.

```
function Get-LargeFolder 
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $False)]
        [ValidateSet('All', 'Calendar', 'Contacts', 'ConversationHistory', 'DeletedItems', 'Drafts', 'Inbox', 'JunkEmail', 'Journal', 'LegacyArchiveJournals', 'ManagedCustomFolder', 'NonIpmRoot', 'Notes', 'Outbox', 'Personal', 'RecoverableItems', 'RssSubscriptions', 'SentItems', 'SyncIssues', 'Tasks')]
        [string]$FolderScope = 'All',
        [Parameter(Mandatory = $False)]
        [int]$Top = 1,
        [Parameter(Mandatory = $False,
                Position = 1,
        ValueFromPipeline = $True)]
        [string]$Identity = '*'
    )

    Get-Mailbox -Identity $Identity -ResultSize Unlimited |
    Get-MailboxFolderStatistics -FolderScope $FolderScope 
}
```

Now I've added a couple lines to get all the mailboxes in my organization (or a specific user's mailbox) which I pipe into a <strong>Get-MailboxFolderStatistics</strong> command with the FolderScope parameter set to the same value we passed to our function. Now we need to sort the results, but, <a href="http://www.workingsysadmin.com/getting-your-organizations-largest-exchange-mailboxes-with-powershell/" target="_blank">see my last post</a> for why that's going to be complicated.

```
function Get-LargeFolder 
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $False)]
        [ValidateSet('All', 'Calendar', 'Contacts', 'ConversationHistory', 'DeletedItems', 'Drafts', 'Inbox', 'JunkEmail', 'Journal', 'LegacyArchiveJournals', 'ManagedCustomFolder', 'NonIpmRoot', 'Notes', 'Outbox', 'Personal', 'RecoverableItems', 'RssSubscriptions', 'SentItems', 'SyncIssues', 'Tasks')]
        [string]$FolderScope = 'All',
        [Parameter(Mandatory = $False)]
        [int]$Top = 1,
        [Parameter(Mandatory = $False,
                Position = 1,
        ValueFromPipeline = $True)]
        [string]$Identity = '*'
    )

    Get-Mailbox -Identity $Identity -ResultSize Unlimited |
    Get-MailboxFolderStatistics -FolderScope $FolderScope |
    Sort-Object -Property @{
        e = {
            $_.FolderSize.split('(').split(' ')[-2].replace(',','') -as [double]
        }
    } -Descending 
}
```

The FolderSize parameter that comes back with a <strong>Get-MailboxFolderStatistics</strong> cmdlet is a string which I'm splitting up in order to get back <em>only</em> the value in bytes which I am casting to a double. Now that we have gathered our stats and put them in order, I just need to select them so they may be returned. Here is the complete script.

```
function Get-LargeFolder 
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $False)]
        [ValidateSet('All', 'Calendar', 'Contacts', 'ConversationHistory', 'DeletedItems', 'Drafts', 'Inbox', 'JunkEmail', 'Journal', 'LegacyArchiveJournals', 'ManagedCustomFolder', 'NonIpmRoot', 'Notes', 'Outbox', 'Personal', 'RecoverableItems', 'RssSubscriptions', 'SentItems', 'SyncIssues', 'Tasks')]
        [string]$FolderScope = 'All',
        [Parameter(Mandatory = $False)]
        [int]$Top = 1,
        [Parameter(Mandatory = $False,
                Position = 1,
        ValueFromPipeline = $True)]
        [string]$Identity = '*'
    )

    Get-Mailbox -Identity $Identity -ResultSize Unlimited |
    Get-MailboxFolderStatistics -FolderScope $FolderScope |
    Sort-Object -Property @{
        e = {
            $_.FolderSize.split('(').split(' ')[-2].replace(',','') -as [double]
        }
    } -Descending |
    Select-Object -Property @{
        l = 'NameFolder'
        e = {
            $_.Identity.Split('/')[-1]
        }
    }, 
    @{
        l = 'FolderSize'
        e = {
            $_.FolderSize.split('(').split(' ')[-2].replace(',', '') -as [double]
        }
    } -First $Top
}
```

Now you can do this.

```
#Get 25 largest Deleted Items folders in your organization
Get-LargeFolder -FolderScope 'DeletedItems' -Top 25

#Get my largest 10 folders
Get-LargeFolder -Identity ThmsRynr -Top 10

#Get the top 25 largest Deleted Items folder for users in a specific group
$arrLargeDelFolders = @()
(Get-ADGroupMember 'GroupName' -Recursive).SamAccountName | ForEach-Object -Process {
    $arrLargeDelFolders += Get-LargeFolder -FolderScope 'DeletedItems' -Identity $_ 
}
$arrLargeDelFolders |
Sort-Object -Property FolderSize -Descending |
Select-Object -Property NameFolder, @{
    l = 'FolderSize (Deleted Items)'
    e = {
        '{0:N0}' -f $_.FolderSize
    }
} -First 25 |
Format-Table -AutoSize
```

&nbsp;
