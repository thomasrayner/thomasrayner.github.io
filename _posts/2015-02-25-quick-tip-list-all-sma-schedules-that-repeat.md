---
layout: post
title: Quick Tip - List All SMA Schedules That Repeat
date: 2015-02-25 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, PowerShell, powershell, PowerShell ISE, powershell ise, SMA, sma]
---
I use a few PowerShell scripts that end up <a title="Quick Tip: Run An SMA Runbook At A Specific Date/Time" href="http://www.workingsysadmin.com/quick-tip-run-an-sma-runbook-at-a-specific-datetime/" target="_blank">triggering Service Management Automation (SMA) runbooks</a>. Each time you want to use PowerShell to do that, you end up creating a one-time use SMA schedule. These one-time schedules are eventually cleaned up by SMA but they can clutter your view pretty well if you have a lot of them.

Luckily, there's an easy way to use PowerShell to list SMA schedules that aren't one-time use. We just want a list of all the SMA schedules that are repeating. You need the <a title="SMA PowerShell Tools" href="http://blogs.technet.com/b/orchestrator/archive/2014/03/11/sma-capabilities-in-depth-the-sma-powershell-module.aspx" target="_blank">SMA PowerShell tools</a> for this.

```
Get-SmaSchedule -WebServiceEndpoint https://SMA-Management-Server | ? { $_.NextRun } | ft
```

We're going to get all the SMA schedules on our SMA implementation and get the ones where there is a NextRun value. The question mark is an alias for the <strong>Where-Object</strong> command and so we're looking for schedules where <em>$_.NextRun</em> is true (has a value, isn't null). I like formatting the output as a table for easier reading.

If a schedule has a NextRun attribute, it's safe to say that it's going to run sometime in the future and is not a one-time use schedule that's already done it's job.
