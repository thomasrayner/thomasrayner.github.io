---
layout: post
title: Quick Tip - Create New LPR Printers Using PowerShell
date: 2015-10-28 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, lpd, lpr, PowerShell, powershell, PowerShell ISE, powershell ise, print, remote admin]
---
There are a bunch of overloads for <strong>Add-Printer</strong> and <strong>Add-PrinterPort</strong> to accommodate different kinds of printers and ports. I found it tough, however, to find real examples of how to use these cmdlets to add LPR printers and ports. Not TCP/IP, not TCPLPR, not local ports. I figured it out, though, and now here's how I did it.

```
foreach ($printer in $(Get-Content -Path 'c:\temp\printers.txt')
{
    Add-PrinterPort -ComputerName PrintServer -PrinterName $printer -HostName 'PrinterHostName'
    Add-Printer -ComputerName PrintServer -DriverName 'Name Of Your Driver' -PortName "PrinterHostName:$printer" -Name $printer
}
```

There are no real surprises here. It's just a matter of finding the right combinations of parameters and their values to make LPR printers and ports happen. In this example, I'm creating a bunch of them out of a list I have in a file.
