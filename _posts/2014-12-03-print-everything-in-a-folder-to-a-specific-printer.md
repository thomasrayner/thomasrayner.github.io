---
layout: post
title: Print Everything In A Folder To A Specific Printer
date: 2014-12-03 14:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, PowerShell, powershell, SMA, sma, WMI, wmi]
---
For one reason or another, I found myself in a situation this week where I needed to print all the contents of a directory on an hourly basis. Not only did I need to print the contents, I needed the jobs to go to a specific printer, too.

SMA runbooks to the rescue! I wrote my solution in PowerShell and stuck it in an inlinescript block in my runbook that I invoked on a print server.

First, I needed to get everything in the directory and print it. I originally looked at using Out-Printer but I have images, PDFs, all kinds of non-plaintext files. I needed another solution and it was this:

```
get-childitem "\\nas\directory" | % { Start-Process -FilePath $_.VersionInfo.FileName –Verb Print -PassThru }\n```

Foreach file in this directory, we're starting a process on the file that prints it. It will effectively open the file in whatever the default application is, render it and print it to your default printer. Great! Except what if I don't want to print to the default printer? The Start-Process cmdlet doesn't seem to lend itself to that very well. As usual, I had to cheat.

```
$defprinter = (Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Default=True").Name
$null = (Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='My Desired Printer'").SetDefaultPrinter()
get-childitem "\\nas\directory" | % { Start-Process -FilePath $_.VersionInfo.FileName –Verb Print -PassThru }
$null = (Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='$defprinter'").SetDefaultPrinter()\n```

Since we're printing to the default printer, why don't we just change the default? Well, because maybe the default printer (that we don't want to print to) is default for a reason. So let's change the default printer and change it back after.

Line 1 gets the name of the default printer. Line 2 sets the default printer to My Desired Printer which is presumably the name of a valid printer on the server. Line 4 sets the default back to whatever the original default was and we already know what line 3 does. Obviously, this is a solution that works in my specific environment that can tolerate a brief interruption to which printer is default.

The rest was easy. I setup a new SMA runbook, invoked the above script on my print server (in an inlinescript block) and scheduled it to run hourly.
