---
layout: post
title: April Fools PowerShell Prank - Write With All The Colors Of The Rainbow
date: 2018-03-28 07:30
author: thmsrynr
comments: true
categories: [april fools, PowerShell, powershell, PSDefaultParameterValues, write-host]
---
Sometimes <strong>Write-Host</strong> gets a bad reputation. Lots of people will repeat inflammatory rhetoric that "Write-Host" kills puppies, and so on, but the only real problem with <strong>Write-Host</strong> is that people use it without knowing what it's for. <strong>Write-Host</strong> is for writing to the console and only the console.

Other cmdlets like <strong>Write-Output</strong> are for writing to standard output which might be the console, or could be somewhere else down the pipeline. <strong>Write-Host</strong>'s output can't be redirected to a log file, isn't useful in unattended execution scenarios, and can't be piped into another command. Lots of people who are new to PowerShell get into a habit of using <strong>Write-Host</strong> when they probably should have used <strong>Write-Output</strong> or something else instead. If you have someone you're trying to train to stop using <strong>Write-Host</strong> when it's not needed, consider this prank, just in time for April Fools Day.

<!--more-->

There's not much to it. Just add a couple of lines to their PowerShell profile.
```
$PSDefaultParameterValues.Add('write-host:foregroundcolor',{get-random $([system.enum]::getvalues([system.consolecolor]))})
$PSDefaultParameterValues.Add('write-host:backgroundcolor',{get-random $([system.enum]::getvalues([system.consolecolor]))})\n```
This adds default values for the <em>-BackgroundColor</em>  and <em>-ForegroundColor</em>  parameters when <strong>Write-Host</strong> is called. If a script specifies a value for those parameters, those specific values will be used instead. If, instead, <strong>Write-Host</strong> is called without specifying values for the foreground and background color parameters, a random one will be used instead. It'll look something like this.

<img class="alignnone wp-image-666 size-full" src="/wp-content/uploads/2018/01/2018-01-10-13_56_29-powershell.png" alt="" width="492" height="509" />
