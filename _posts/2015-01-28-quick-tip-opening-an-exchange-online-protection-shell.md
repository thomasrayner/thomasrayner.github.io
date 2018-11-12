---
layout: post
title: Quick Tip - Opening An Exchange Online Protection Shell
date: 2015-01-28 02:15
author: thmsrynr@outlook.com
comments: true
categories: [Exchange, exchange, PowerShell, powershell, PowerShell ISE, powershell ise]
---
There's lots of big, exciting, non-blogable things happening at work this week so here's a very quick tip.

Last week I wrote a post on <a title="Opening A Remote Exchange Management Shell" href="http://www.workingsysadmin.com/opening-a-remote-exchange-management-shell/" target="_blank">a PowerShell function I threw in my profile to connect quickly to Exchange</a>. That's great, but what if you also want to manage Exchange Online Protection (EOP) from a PoweShell console? Well it turns out to be pretty easy.

```
$cred = Get-Credential
$s = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $cred -Authentication Basic -AllowRedirection
import-pssession $s\n```

This looks a lot like the function I showed you last week except it's connecting to Office 365 and you need to use your Live ID instead of AD credentials.
