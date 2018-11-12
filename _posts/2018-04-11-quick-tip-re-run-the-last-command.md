---
layout: post
title: Quick Tip: Re-Run The Last Command
date: 2018-04-11 08:30
author: thmsrynr
comments: true
categories: [beginner series, PowerShell, powershell, quick tip, quick tips]
---
Sometimes, while you're poking around in the console, you want to re-run the last command. Sure, you can hit the up arrow and enter, but PowerShell always gives you multiple ways to do things.

<!--more-->

It's easy, using the <strong>Invoke-History</strong> cmdlet. You can also use its alias which is just <strong>r</strong>. Running that cmdlet without any parameters will run the last command from the console. Alternatively, you can specify a value for the ID parameter, and run one from further back in your history.

How do you find out what those IDs should be? Using <strong>Get-History</strong> to see everything you've run in this session, and the ID number for that command.
