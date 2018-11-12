---
layout: post
title: Quick Tip - Get All SMA Runbook Schedules That Will Run Between Now And Then
date: 2014-12-17 16:15
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, PowerShell, powershell, SMA, sma]
---
I wanted to do some maintenance on my SMA runbook servers but couldn't remember which jobs were going to run in the next 12 hours (if any). Luckily there's a quick way of getting that information! This work assumes that you have the <a title="SMA Tools" href="http://blogs.technet.com/b/orchestrator/archive/2014/03/11/sma-capabilities-in-depth-the-sma-powershell-module.aspx" target="_blank">SMA tools installed</a> and that you ran the below command or have it as part of your profile.

```
import-module Microsoft.SystemCenter.ServiceManagementAutomation\n```

Behold!

```
get-smaschedule -WebServiceEndpoint "https://your-server" | ? { $_.NextRun -gt (get-date).date -and $_.NextRun -lt (get-date).addhours(12)}\n```

This isn't a very crazy command. "your-server" is the server where you have the SMA management items installed, not an individual runbook server.

You're getting all the SMA schedules from your SMA instance and filtering for items whose next run is after "now" and before "now plus 12 hours". You can change the get-date related items easily to suit your needs. For instance, what ran last night? What will run tomorrow? What ran on October 31?

&nbsp;
