---
layout: post
title: Quick Tip: Allow A Null Value For An Object That Doesn't Normally Allow It
date: 2016-09-14 08:30
author: thmsrynr@outlook.com
comments: true
categories: [null values, nullable, PowerShell, powershell, quick tip]
---
In the PowerShell Slack channel (<a href="http://powershell.slack.com" target="_blank">powershell.slack.com</a>) a question came up along the lines of "I have a script that needs to pass a datetime object, but sometimes I'd like that datetime object to be null". Never mind that maybe the script could be re-architected. Let's solve this problem.

The issue is, if you try to assign a null value to a datetime object, you get an error.

<pre class="lang:ps decode:true ">[datetime]$null
Cannot convert null to type "System.DateTime".</pre>

The solution is super easy. Just make the thing nullable.

<pre class="lang:ps decode:true ">[nullable[datetime]]$null</pre>

This will return no output. So when you're declaring the variable that will hold your datetime object, just make sure you make it nullable.

<pre class="lang:ps decode:true ">[nullable[datetime]]$date = $MaybeNullMaybeNot</pre>

Just for more proof this works as advertised, try this.

<pre class="lang:ps decode:true ">try { [datetime]$null; write-output 'worked!' } catch { write-output 'no worked!' }
no worked!

try { [nullable[datetime]]$null; write-output 'worked!' } catch { write-output 'no worked!' }
worked!</pre>

Cool!
