---
layout: post
title: Quick Tip - Run An SMA Runbook At A Specific Date/Time
date: 2014-12-30 02:15
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, PowerShell, powershell, SMA, sma]
---
Happy New Year's Eve! Here's a quick tip just before New Year's.

I recently answered <a title="Scheduling in SMA from a powershell script" href="https://social.technet.microsoft.com/Forums/en-US/3502b7cc-b17d-4afd-b206-16f20156b6e3/scheduling-in-sma-from-a-powershell-script?forum=scogeneral" target="_blank">a question on Technet about scheduling SMA runbooks</a>. It's no secret that the scheduling engine in Service Management Automation leaves something to be desired. Here's how I like to use PowerShell to get specific about when an SMA runbook is going to be triggered.

You'll need the <a title="SMA PowerShell Tools" href="http://blogs.technet.com/b/orchestrator/archive/2014/03/11/sma-capabilities-in-depth-the-sma-powershell-module.aspx" target="_blank">SMA PowerShell tools</a> installed and imported for this to work.

```
$dateWhen = [DateTime]"&lt;put a date and time in here or otherwise calculate one&gt;"
$strSchedName = "some_prefix_$($strWhen)"
$schedRun = set-smaschedule -name $strSchedName -webserviceendpoint "https://your-endpoint" -scheduletype onetimeschedule -starttime $dateWhen -expirytime $dateWhen.AddHours(3) -description $env:username
$strReturn = start-smarunbook -name "your-runbook" -WebServiceEndpoint "https://your-endpoint" -schedulename $strSchedName -parameters @{ var1 = "var1"; var2 = "var2" }
```

Line 1 is easy, it's just a variable for a datetime object and it's going to represent the time you want to trigger the runbook. Line 2 is a variable for what the name of the SMA schedule asset will be. I like to add something dynamic here to avoid naming collisions.

Now the interesting parts. On Line 3, we're creating an SMA schedule asset using <strong>set-smaschedule</strong>. It's going to be named our Line 2 variable, it's going to be a onetimeschedule (instead of recurring), start at our start time (Line 1) and expire three hours after the start time. On Line 4, I'm triggering the runbook with <strong>start-smarunbook</strong> and specifying the schedule we created on Line 3. I'm also passing parameters in a hash table.

You're done! The only hiccup with this I've seen is if one of your parameters for your runbook is a hashtable. <a title="Passing Hashtables to Start-SMARunbook as a Parameter" href="http://sysjam.wordpress.com/2014/12/23/passing-hashtables-to-start-smarunbook-as-a-parameter/" target="_blank">Matthew at sysjam.wordpress.com covered this weird situation in a blog post very recently.</a>
