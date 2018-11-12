---
layout: post
title: Cheating To Fix Access Is Denied Error Using Get-WMIObject
date: 2014-11-19 15:37
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, PowerShell ISE, powershell ise, WMI, wmi]
---
I was doing a little work that involved using PowerShell to get a list of printers from several remote print servers. I figured this would be a great job for WMI and I was right. The command I used, looked like this.

<pre class="wrap:true lang:ps decode:true ">$printserver = "printserver1.domain.tld"
Get-WMIObject -class Win32_Printer -computer $printserver | Select Name,DriverName,PortName | Export-CSV -path 'C:\temp\$printserver.csv'</pre>

I had a list of print servers that I imported into an array and looped through them but this is the important part of the code. I am simply using WMI to get some information about the logical printer objects on a given print server and exporting them to a CSV.

How boring! This isn't a very old blog but we usually talk about more complicated things than that. Well things got weird on one print server that we'll simply call PrintServer2. PrintServer2 threw an error instead of working nicely.

<pre class="wrap:true lang:ps decode:true ">Get-WMIObject : Access is denied. (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
At line:1 char:1
+ Get-WMIObject -class Win32_Printer -computer PrintServer2 | Select Name,DriverName,Por ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Get-WmiObject], UnauthorizedAccessException
    + FullyQualifiedErrorId : System.UnauthorizedAccessException,Microsoft.PowerShell.Commands.GetWmiObjectCommand
</pre>

Not cool. I have Domain Admin rights... it's a domain joined server... what do you mean access is denied? Running the command locally on the server worked, I just couldn't do it remotely. There's <a title="Search for the answer" href="http://lmgtfy.com/?q=Get-WMIObject+%3A+Access+is+denied.+(Exception+from+HRESULT%3A+0x80070005+(E_ACCESSDENIED))" target="_blank">plenty of literature on trying to fix this error</a> already but I was in a hurry so I tried the next thing that came to mind: cheat a bit and run the command locally on the server... remotely.

<pre class="wrap:true lang:ps decode:true ">$printserver = "printserver2.domain.tld"
invoke-command -computer $printserver -scriptblock { Get-WMIObject -class Win32_Printer -computer localhost | Select Name,DriverName,PortName } | Export-CSV -path 'C:\temp\$printserver.csv'</pre>

I didn't do anything ground breaking, I just used invoke-command to run the command on the server instead of running the command on my local machine (to retrieve remote information).

Hah! I beat you, stupid Windows Server 2003 box that has been around since I was in junior high school and needs to be decommissioned! I got your printer information from you without having to fix any of your weird problems!

The moral of the story is that sometimes, you can cheat a little bit to accomplish your goal and avoid doing a whole bunch of terrible patches, regedits, etc. to your infrastructure.
