---
layout: post
title: Quick Tip - Did the last command work or not?
date: 2018-02-07 07:30
author: thmsrynr
comments: true
categories: [beginner series, beginner series, PowerShell, powershell, quick tip]
---
In PowerShell, there is usually at least a few ways to do most tasks and detecting if the last command resulted in an error or if it worked is no exception. You could wrap code in a try/catch block, but sometimes that's overkill. Regardless of your reason for wanting to get the work/borked status of the last command, here are a couple simple ways of doing it.

<!--more-->

The <strong>Get-History</strong> cmdlet is a great way to get this and other information for commands you executed in your current session. If you run it, you'll get an ID and a "CommandLine" which is the command that you ran, but if you pipe into <strong>Select-Object -Property *</strong>, you'll see that there's also an ExecutionStatus and times for start and end. That ExecutionStatus is what you're looking for in this case.

If you just run <strong>Get-History | Select *</strong> then you'll get those pieces of information for every command you ran in your current session. If you only want to see the information for the last command you ran, just remember that you're working with an array and run <strong>(Get-History)[-1] | Select *</strong>. That will get the last item in the array of command information returned by Get-History and show you that info.

If you truly just want to know if the last command completed successfully or not, there's a special variable built into PowerShell for it. It's <strong>$?</strong>. Just type <strong>$?</strong> into your console and you'll get back either True or False, a boolean value for if the last command completed successfully or not. Pretty handy shortcut, no?
