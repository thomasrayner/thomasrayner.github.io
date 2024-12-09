---
layout: post
title: Happy Birthday To Me!
date: 2016-03-30 08:30
author: thmsrynr@outlook.com
comments: true
categories: [nshr, Uncategorized]
---
Today is my birthday and so I don't feel like doing a whole ton of work. I do, however, feel like celebrating. Obviously that means singing Happy Birthday. That should be a pretty easy PowerShell task. In fact, it's made even easier by the fact that fellow Microsoft MVP <a href="https://twitter.com/pcgeek86" target="_blank">Trevor Sullivan</a> already wrote and shared a script to do it. Here it is on the Microsoft Script Gallery: <a href="https://gallery.technet.microsoft.com/A-PowerShell-Happy-983c1253" target="_blank">https://gallery.technet.microsoft.com/A-PowerShell-Happy-983c1253</a>.

He's got an array of hash tables which each consist of a pitch and a length. The <strong>[System.Console]::Beep()</strong> method just so happens to take a pitch and length parameter. Predictably, this method makes the computer speaker beep. Even if you don't have speakers, this should still work. All the pitches and lengths correspond to the pitch of a beep and how long it should last.
