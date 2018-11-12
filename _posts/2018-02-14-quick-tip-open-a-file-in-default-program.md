---
layout: post
title: Quick Tip: Open A File In Default Program
date: 2018-02-14 07:30
author: thmsrynr
comments: true
categories: [beginner series, filepath, filesystem, open file, PowerShell, powershell, start-process]
---
When you double click a file in Explorer.exe, it automatically opens in its default program if it has one associated with its type. But did you know you can do the same thing using PowerShell?

<!--more-->

Most people are aware of <strong>Start-Process</strong>, the PowerShell cmdlet for starting processes on the computer, but most people just use it for executing things they'd normally just look to run in cmd.exe like installers. But <strong>Start-Process</strong> has a <em>-FilePath</em> parameter that you can use to open a file in its default program.
<pre class="lang:default decode:true ">Start-Process -FilePath C:\temp\opens-in-excel.csv</pre>
On my computer, this command opens the given CSV in Excel. This is handy in situations where you're poking around in the console, exporting files, and then perhaps you wish to open that file and rather than clicking around inefficiently through Explorer.exe, you can just launch it from the PowerShell CLI.
