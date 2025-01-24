---
layout: post
title: My Demonstration Prompt
date: 2017-05-03 08:30
author: thmsrynr@outlook.com
comments: true
categories: [ansi, i &lt;3 powershell, PowerShell, powershell, prompt, prompt]
---
Recently, I have found myself doing a lot of CLI PowerShell demos. Normally, I have a prompt that uses <a href="https://github.com/jaykul/powerline" target="_blank" rel="noopener noreferrer">Joel Bennet's PowerLine module</a> and looks like this.

<a href="http://www.workingsysadmin.com/wp-content/uploads/2017/04/2017-04-03-09_40_44-powershell.png"><img class="alignnone size-full wp-image-456" src="http://www.workingsysadmin.com/wp-content/uploads/2017/04/2017-04-03-09_40_44-powershell.png" alt="" width="585" height="107" /></a>

In my opinion, it's pretty cool looking, and it gives me a bunch of useful information including the Get-History ID of the line that I ran, the nested prompt level, current drive, the present working directory, the time the last command took to run and whether it was successful, and the current time.

This is way too much information for a regular demo, and ends up in me answering questions about my prompt and explaining it for 5 minutes which eats up valuable demo time. Here's my new demo prompt.

<!--more-->

<a href="http://www.workingsysadmin.com/wp-content/uploads/2017/04/2017-04-03-09_43_21-powershell.png"><img class="alignnone size-full wp-image-457" src="http://www.workingsysadmin.com/wp-content/uploads/2017/04/2017-04-03-09_43_21-powershell.png" alt="" width="282" height="65" /></a>

Not much explaining to do here. Here's the code I have in my profile to make it happen.

```
function Invoke-DemoPrompt {
    $demo = 'function prompt {"I $([char]0x1b)[0;31m$([char]9829) $([char]0x1b)[0;0mPS&gt; "} clear-host'
    Invoke-Expression $demo
}
```

Shout out to Joel and Brandon in the PowerShell Slack for working this one out. It's pretty simple. $demo is a string that redefines my prompt function and its invoked.
