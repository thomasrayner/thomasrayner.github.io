---
layout: post
title: Bypassing PowerShell Execution Policy
date: 2015-03-11 08:30
author: thmsrynr@outlook.com
comments: true
categories: [execution policy, executionpolicy, PowerShell, powershell, PowerShell ISE, powershell ise]
---
<strong>Let me be absolutely clear about this post. I do not in any way encourage or support people who wish to use the below information to circumvent the controls put in place by companies and administrators. This post is strictly for academic purposes and for the sake of sharing information.</strong>

PowerShell Execution Policies control whether or not a system may run a PowerShell script based on whether the script is signed or not. See the<a title="about_Execution_Policies" href="https://technet.microsoft.com/en-ca/library/hh847748.aspx" target="_blank"> about_Execution_Policies Technet page</a> for more information if you are unfamiliar with execution policies or how to apply them. Execution policies do not, however, limit a user or service from running commands in a PowerShell shell (PowerShell.exe).

So what if you have an unsigned script you want to run but your execution policy is preventing it? Well, there's a way to bypass the execution policy. And it's run from a PowerShell shell.

Administrative users can easily bypass the execution policy with this command.

```
PowerShell.exe -noprofile -executionpolicy bypass -file "\\path\to\file.ps1"
```

But what about limited users? Well there's something for them, too.

```
Powershell.exe -NoProfile -Command {.([scriptblock]::create((Get-Content "\\path\to\script.ps1" | out-string)))}
```

That's right, just one line. No registry hacking, no weird developer program strangeness, just a command that allows a user or service to subvert the execution policy of the machine.

Let's break down the command. We're launching PowerShell.exe, not exactly a puzzler. We want it with no profile and we're telling it to run a command. The trick is that the command we're running is effectively going to be the script that our execution policy would otherwise block.

The dot is basically an alias for "execute" and in this case, we're telling it to execute what's in the proceeding round brackets. The round brackets contain instructions to create a new ScriptBlock out of the contents of the .ps1 file that the execution policy would otherwise prevent from running.

I think it's clear that this is not really something that Microsoft intends for you to do. Use (or not) wisely at your own discretion.
