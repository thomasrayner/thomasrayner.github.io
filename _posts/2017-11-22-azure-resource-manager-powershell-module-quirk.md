---
layout: post
title: Azure Resource Manager PowerShell Module Quirk
date: 2017-11-22 07:00
author: thmsrynr@outlook.com
comments: true
categories: [Azure, azure, azure automation, azure automation, azurerm, PowerShell, powershell]
---
If you've used the Azure Resource Manager (AzureRM) PowerShell module much, you may have noticed it may sometimes behave strangely. In this post, I'm going to share one that had me stuck for longer than I care to admit...

<!--more-->

So, here's the situation. I was working in the PowerShell console, looking to enumerate the automation schedules (that kick off Azure Automation runbooks) in one automation account. I ran this command to get started.

```
Get-AzureRmAutomationSchedule -ResourceGroupName 'my-rg' -AutomationAccountName 'my-aa'
```

I got predictable output, too. Here's the example output for one of the schedules.

```
StartTime              : 9/30/2017 12:01:00 PM -06:00
ExpiryTime             : 12/31/9999 4:59:00 PM -07:00
IsEnabled              : True
NextRun                : 11/30/2017 12:01:00 PM -07:00
Interval               : 1
Frequency              : Month
MonthlyScheduleOptions :
WeeklyScheduleOptions  :
TimeZone               : America/Denver
ResourceGroupName      : my-rg
AutomationAccountName  : my-aa
Name                   : General Name
CreationTime           : 9/20/2017 10:26:26 AM -06:00
LastModifiedTime       : 9/20/2017 10:26:26 AM -06:00
Description            :
```

There's just one problem. I know for a fact this schedule runs on the last day of every month, and includes data in the MonthlyScheduleOptions field which is empty above. What gives?

Well, as it turns out, the monthly and weekly schedule options are only returned if you specify a specific automation schedule like this.

```
Get-AzureRmAutomationSchedule -ResourceGroupName 'my-rg' -AutomationAccountName 'my-aa' -name 'General Name'
```

Now I get this output.

```
StartTime              : 9/30/2017 12:01:00 PM -06:00
ExpiryTime             : 12/31/9999 4:59:00 PM -07:00
IsEnabled              : True
NextRun                : 11/30/2017 12:01:00 PM -07:00
Interval               : 1
Frequency              : Month
MonthlyScheduleOptions : Microsoft.Azure.Commands.Automation.Model.MonthlyScheduleOptions
WeeklyScheduleOptions  : Microsoft.Azure.Commands.Automation.Model.WeeklyScheduleOptions
TimeZone               : America/Denver
ResourceGroupName      : my-rg
AutomationAccountName  : my-aa
Name                   : General Name
CreationTime           : 9/20/2017 10:26:26 AM -06:00
LastModifiedTime       : 9/20/2017 10:26:26 AM -06:00
Description            :
```

That on it's own isn't useful because it's just showing me the type of object that's there, but I can do something like this to get more meaningful output (for my purposes here).

```
Get-AzureRmAutomationSchedule -ResourceGroupName 'my-rg' -AutomationAccountName 'my-aa' -name 'General Name' | select Name,@{l='DaysOfMonth'; e={$_.MonthlyScheduleOptions.DaysOfMonth}}
```

And get output like this.

```
Name                     DaysOfMonth
----                     -----------
General Name             LastDay
```

There's more elements in weekly and monthly schedule options than I'm using here, but this is just to highlight the behavior of the <strong>Get-AzureRmAutomationSchedule</strong> cmdlet. If you don't specify a value for <em>-Name</em> parameter, then you won't get all the information back about the schedules you're seeing.

By the way, there are plenty of other AzureRM cmdlets that work this way. So, if you're working with Azure in PowerShell and wondering why the AzureRM module doesn't seem to be giving you all the data that it should, check for the presence of this quirk.
