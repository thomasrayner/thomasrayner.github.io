---
layout: post
title: Using PowerShell To Simulate A Ransomware Attack
date: 2015-11-11 08:30
author: thmsrynr@outlook.com
comments: true
categories: [file system, PowerShell, powershell, PowerShell ISE, powershell ise, ransomware, security]
---
Disclaimer: There are tons of different ransomware variants which behave in tons of different ways. This is an example of simulating just one of those behaviors - one that I've found to be common.

&nbsp;

It's a commonly held belief that there's nothing you can do to guarantee you'll never be hit by <a href="http://en.wikipedia.org/wiki/Ransomware" target="_blank">a ransomware attack</a>, you can only be prepared with systems and processes to detect one, stop it, and recover from it. If you're putting in some sort of system to detect a ransomware attack, you'd probably be wise to test it, but how? Installing ransomware is not something I'd recommend.

A common way of detecting a ransomware attack is monitoring a file system for a series of conditions. This is one such way you might configure these conditions:

<ol>
    <li>A user modifies more than 100 files</li>
    <li>A user renames more than 100 files</li>
    <li>1 and 2 happen in under 60 seconds</li>
</ol>

This works nicely because ransomware will usually encrypt a file (modifying it) and append an extension (renaming it) in a short amount of time. You might have some false positives with this, or you might want to make the conditions more strict or lenient but hey, it's my blog and this is what I am testing with.

So how do you simulate this behavior with PowerShell? Like this.

<pre class="lang:ps decode:true  ">$strDir = "C:\temp\test1\"
GCI $strDir | Remove-Item -Force
1..200 | % { $strPath = $strDir + $_ + ".txt"; "something" | Out-File $strPath | Out-Null }
Measure-Command { 1..101 | % { $strPath = $strDir + $_ + ".txt"; $strNewPath = $strPath + ".chng"; "changed" | Out-File -Append $strPath; Rename-Item -Path $strPath -NewName $strNewPath } }</pre>

Lines 1, 2 and 3 setup the environment. $strDir is the location we're monitoring for ransomware attacks (or a test directory in this case). Line 2 empties the test directory which you probably don't want to do indiscriminately in a production area but I want to do in my test area.

Line 3 creates 200 txt files in $strDir. <strong>1..200</strong> is a slick way of writing all the numbers between 1 and 200 inclusive. Try it yourself in a PowerShell console. Then, for each of those numbers, we're creating a file and suppressing the output.

Line 4 is the ransomware simulation. For 101 files, we're making a variable $strPath which is an individual file we created in line 3. We're also crafting a new path stored in $strNewPath which is the same file but with an extension. Then I'm changing the contents of the file by writing "changed" inside it. Finally, I rename the file. The whole thing is wrapped in a <strong>Measure-Command</strong> block so I can see how long it takes. On my test system, the ransomware part took 688 ms.

<pre class="">Days              : 0
Hours             : 0
Minutes           : 0
Seconds           : 0
Milliseconds      : 688
Ticks             : 6887630
TotalDays         : 7.97179398148148E-06
TotalHours        : 0.000191323055555556
TotalMinutes      : 0.0114793833333333
TotalSeconds      : 0.688763
TotalMilliseconds : 688.763
</pre>

There you go! Try it yourself and see if you can detect this simulated ransomware attack.
