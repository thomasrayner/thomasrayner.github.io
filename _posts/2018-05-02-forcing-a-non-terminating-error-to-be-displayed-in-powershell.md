---
layout: post
title: Forcing A Non-Terminating Error To Be Displayed In PowerShell
date: 2018-05-02 07:30
author: thmsrynr
comments: true
categories: [error handling, PowerShell, powershell, user experience]
---
In full disclosure, this post contains information that a user experience expert might frown at. I'm not really sure, since I'm not a user experience expert. I do know a lot about PowerShell, however, and that's really what this post is about.

Say you have users of your scripts and modules who might have their <strong>$ErrorActionPreference</strong> set to SilentlyContinue or maybe you know for a fact that your code explicitly sets it that way. That's probably another thing that will make the user experience pros mad but here you are anyway. Let's just say that your stakeholders FORCED you to do it. What happens if you absolutely need to, have to, must display a non-terminating error, such as those you create with <strong>Write-Error</strong>? Here's one option.

<!--more-->

You could store the current Error Action Preference in another variable, set the EAP to "stop" or "continue" and then write your error, and then set the EAP back, but there's a simpler way!

<strong>Write-Error</strong>, like pretty much anything else, has an -ErrorAction parameter which determines what PowerShell will do if the cmdlet it's attached to throws an error out. Since <strong>Write-Error</strong> will, by definition, throw an error every time you run it, the -ErrorAction becomes pretty important if you want to use it here.

Even if the Error Action Preference is set to SilentlyContinue, you can do this...
```
Write-Error "This is my error" -ErrorAction Continue
```
... and your error will be written to the screen anyway. Obviously you can use the -ErrorAction parameter on everything else that has one too, for the same effect. Error Action Preference is just there to determine how errors are handled if you don't specify -ErrorAction.
