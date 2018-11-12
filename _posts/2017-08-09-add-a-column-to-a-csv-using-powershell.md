---
layout: post
title: Add A Column To A CSV Using PowerShell
date: 2017-08-09 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, csv, export-csv, import-csv, PowerShell, powershell, string manipulation, working with data]
---
Say you have a CSV file full of awesome, super great, amazing information. It's perfect, except it's missing a column. Luckily, you can use <strong>Select-Object</strong> along with the other CSV cmdlets to add a column.

In our example, let's say that you have a CSV with two columns "ComputerName" and "IPAddress" and you want to add a column for "Port3389Open" to see if the port for RDP is open or not. It's only a few lines of code from being done.

<!--more-->

```
PS&gt; $servers = Import-Csv C:\Temp\demo\servers.csv

PS&gt; $servers

Name     IPAddress
----     ---------
server01 10.1.2.10
server02 10.1.2.11\n```

Now, let's borrow some code from my <a href="http://www.workingsysadmin.com/calculated-properties-in-powershell/" target="_blank" rel="noopener noreferrer">post on calculated properties in PowerShell</a> to help us add this column and my post on <a href="http://www.workingsysadmin.com/use-test-netconnection-in-powershell-to-see-if-a-port-is-open/" target="_blank" rel="noopener noreferrer">seeing if a port is open using PowerShell</a> to populate the data.

```
PS&gt; $servers = $servers | Select-Object -Property *, @{label = 'Port3389Open'; expression = {(Test-NetConnection -ComputerName $_.Name -Port 3389).TcpTestSucceeded}}\n```

You can run <strong>$servers</strong> to see the if the new data shows up correctly (spoiler alert, it did), and then use <strong>Export-Csv</strong> to put the data into the same, or a new CSV file.

```
PS&gt; $servers | Export-Csv -Path c:\temp\demo\servers-and-port-data.csv -NoTypeInformation\n```

Use the <em>-Force</em> flag if you're overwriting an existing CSV.
