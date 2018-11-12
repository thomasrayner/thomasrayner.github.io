---
layout: post
title: How To Tell If The Verbose Parameter Of A Function Is From [CmdletBinding()] Or Manually Added
date: 2017-03-01 08:30
author: thmsrynr@outlook.com
comments: true
categories: [cmdletbinding, PowerShell, powershell, verbose]
---
Pardon the long title. I had a task recently to go through a big folder full of scripts written by random people with equally random skill levels. Lots of the scripts had a <strong>-Verbose</strong> parameter, but they weren't all done correctly.

Some scripts correctly included the <strong>[CmdletBinding()]</strong> line above the <strong>param()</strong> block. Some just had a<strong> [Switch]$Verbose</strong> parameter (wrong). Others had <em>both </em>(double wrong, script won't even run).

Consider the following three functions, which illustrate the three categories I was dealing with.

<!--more-->

<pre class="lang:ps decode:true ">function do-verbose1 { param([switch]$Verbose) @{} + $psboundparameters }                  
function do-verbose2 { [cmdletbinding()] param() @{} + $psboundparameters }                
function do-verbose3 { [cmdletbinding()] param([switch]$Verbose) @{} + $psboundparameters }</pre>

The first one is bad, the second one is good, the third one is double bad.

Here's a quick way you can check the scripts using PowerShell so you don't have to open them all up.

<a href="http://www.workingsysadmin.com/wp-content/uploads/2016/12/2016-12-06-09_41_54-powershell.png"><img class="alignnone size-full wp-image-417" src="http://www.workingsysadmin.com/wp-content/uploads/2016/12/2016-12-06-09_41_54-powershell.png" alt="2016-12-06-09_41_54-powershell" width="915" height="414" /></a>

As you can see, the first one has a parameter of <strong>-Verbose</strong> so <strong>Get-Help</strong> will show you info about it. The second one returns nothing. The third one returns an error.

For checking real scripts that have other parameters, you should pipe the results into <strong>where-object { $_.Name -eq 'Verbose' }</strong> to eliminate other parameters from being returned.
