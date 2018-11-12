---
layout: post
title: My July 2015 Scripting Puzzle Solution
date: 2015-07-06 09:22
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, powershell.org, Scripting Puzzle, scripting puzzle, WMI, wmi]
---
If you haven't heard, PowerShell.org is taking the lead on organizing the PowerShell Scripting Games. There's a new format that involves monthly puzzles. Here's their post on July's puzzle: <a href="http://powershell.org/wp/2015/07/04/2015-july-scripting-games-puzzle/" target="_blank">http://powershell.org/wp/2015/07/04/2015-july-scripting-games-puzzle/</a>

Here's my solution. I did the extra challenges, as well except for the optional "go obscure, use aliases" challenge. I didn't submit my solution, I just do them for funsies and to share my solutions on my blog.

```
$Computers = @('comp1','comp2'); Get-WmiObject -Class Win32_OperatingSystem -ComputerName $Computers | Format-Table PSComputerName,ServicePackMajorVersion,Version,@{N='BIOSSerial';E={$(Get-WMIObject -Class Win32_BIOS -ComputerName $_.PSComputerName).SerialNumber}}\n```

The first thing I'm doing is defining an array of computer names which could have come from anywhere. Then, technically on the next line since there's a semicolon, I have my command. It's just a <strong>Get-WMIObject</strong> on the <em>Win32_OperatingSystem</em> class. The <em>ComputerName</em> parameter takes an array which is basically a built in <strong>ForEach-Object</strong> loop, satisfying the second and third challenge requirements. I pipe the results into a <strong>Format-Table </strong>command for easy reading but we're not out of the woods yet. I select the PSComputername, ServicePackMajorVersion and Version properties pretty obviously but the last item, BIOSSerial looks strange.

The SerialNumber property in the <em>Win32_OperatingSystem  </em>WMI object is different than the SerialNumber property in the <em>Win32_BIOS</em> WMI object. The puzzle clearly requests the BIOS serial number, so I created a <a href="https://technet.microsoft.com/en-ca/library/ee692794.aspx" target="_blank">custom table</a> column which retrieved the BIOS serial number. <em><strong>Technically speaking</strong></em> the only semicolon I use in this solution comes from the custom table command. I'm not counting the one that separates the definition of $Computers from the real command. I could have changed it to look like this, but I thought my solution was more readable.

```
Get-WmiObject -Class Win32_OperatingSystem -ComputerName @('comp1','comp2')\n```

Good puzzle! I don't do a ton with WMI or custom tables so this was weird for me, even if it was a relatively simple puzzle.
