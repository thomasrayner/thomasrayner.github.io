---
layout: post
title: Quick Tip - Get-Random Is Weird - Doesn't Include The Maximum Value
date: 2015-02-18 08:30
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, PowerShell ISE, powershell ise]
---
The PowerShell command <strong>Get-Random</strong> is kind of weird. Consider the following script:

<pre class="lang:ps decode:true">while ($true)
{
    Get-Random -Minimum 1 -Maximum 2
    sleep 1
}</pre>

Run it on your own computer. Every second, it should write a random number between 1 and 2 until you interrupt it (CTRL + C). You would expect a somewhat balanced output of 1's and 2's like if you were recording the outcomes of repeatedly flipping a coin. Right? Wrong. You will get a string of 1's and never ever EVER get a 2. Change the Maximum to 3 and you will get 1's and 2's but no 3's.

Apparently the maximum value of the <strong>Get-Random</strong> command isn't a valid value to return, but, the minimum is. It's possible that there is a condition where the command will work as expected but I haven't experimented enough to know for sure.

Weird.
