---
layout: post
title: My September 2015 Scripting Puzzle Solution
date: 2015-09-08 07:10
author: thmsrynr@outlook.com
comments: true
categories: [get-wmiobject, PowerShell, powershell, Scripting Puzzle, scripting puzzle, scriptingpuzzle, Uncategorized, WMI]
---
If you haven’t heard, PowerShell.org is taking the lead on organizing the PowerShell Scripting Games. There’s a new format that involves monthly puzzles. Here’s their post on September's puzzle: <a href="http://powershell.org/wp/2015/09/05/september-2015-scripting-games-puzzle/" target="_blank">http://powershell.org/wp/2015/09/05/september-2015-scripting-games-puzzle/</a>

Here is my solution. The summarized instructions are: "You have a CSV with one column, "machinename", and you need to return the friendly OS name for each. They're a mix of machines dating back to WinXP. All have PowerShell 2.0 or better and WinRM is open between you and each host. Try to limit your usage of curly braces."

I did this.

```
Import-Csv -Path $InputFile | ForEach-Object -Process { Get-WmiObject Win32_OperatingSystem -ComputerName $_.MachineName | Select-Object -Property PSComputerName, Caption } | Export-Csv -Path $OutputFile -NoTypeInformation
```

It's pretty verbose but I made it that way for readability. I use a grand total of one pair of curly braces in the solution, which I hope satisfies the definition of "limited". What I'm doing is importing the CSV, which is located wherever $InputFile is, and for each of the lines in that CSV, I am performing a task on the computer indicated. That task is to get the Win32_OperatingSystem WMI Object which contains all kinds of neat info about a system's OS. Of the data returned, I am selecting the PSComputerName, which should equal the same value as the line in the input file (but doesn't cost me any curly braces to return) and the Caption, which is the friendly name of the OS. I export that into $OutputFile's location.

Fun times!
