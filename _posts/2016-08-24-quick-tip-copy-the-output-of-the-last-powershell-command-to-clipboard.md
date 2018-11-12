---
layout: post
title: Quick Tip - Copy The Output Of The Last PowerShell Command To Clipboard
date: 2016-08-24 08:30
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, PowerShell 5.0, powershell 5.0, profile]
---
I recently found myself poking around in PowerShell and going "oh, good now I want to copy and paste that output into an email/dialog box/tweet/notepad/another script/complaint box" and either trying to copy and paste it out of PowerShell or hitting the up arrow and piping whatever the last command was into <strong>Set-Clipboard</strong>. What a hassle.

So, I threw this small function into my profile.

```
function cc { r | scb }\n```

You'll need PowerShell 5.0 for this one (for <strong>Set-Clipboard</strong>). This just looks like gibberish though, what's going on?

Well, clearly I'm defining a function named <strong>cc</strong> which is not a properly named PowerShell function but I'm being lazy. What does it do? Well it does <strong>r | scb</strong>.

<strong>r</strong> is an alias for <strong>Invoke-History</strong> which re-runs the last command you typed. Try it yourself.

```
PS G:\&gt; write-output "hah!"
hah!

PS G:\&gt; r
write-output "hah!"
hah!

PS G:\&gt; r
write-output "hah!"
hah!\n```

<strong>scb</strong> is an alias for <strong>Set-Clipboard</strong> which means whatever came out of the last command will be the new contents of your clipboard.

The cool thing about this is it doesn't just have to be text. <a href="http://www.workingsysadmin.com/new-stuff-get-clipboard-and-set-clipboard-new-in-powershell-5-0/" target="_blank">Check out my other post about all the things <strong>Set-Clipboard</strong> can do.</a>
