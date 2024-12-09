---
layout: post
title: Quick Tip - Get All The Security Patches Installed On A Server Since A Specific Date
date: 2016-10-26 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, patches, patching, PowerShell, powershell, string manipulation, string manipulation, WMI, wmi]
---
Recently, I needed to get a list of all the security patches I'd installed on a group of servers in the last year. It turns out that there's a WMI class for this and it's super easy to retrieve this info.

```
get-wmiobject win32_quickfixengineering -ComputerName $CompName | ? { $_.InstalledOn -gt (get-date).addyears(-1) }
```

In the <em>win32_quickfixengineering</em> class, you'll find all the security patches installed on a system. One of the properties is the <em>InstalledOn</em> attribute which more recent than a year ago.

If you have a list of servers to do this for, this is still really easy.

```
$svrs = @"
server1
server2
server3
"@

$svrs.split("`n") | % { get-wmiobject win32_quickfixengineering -ComputerName $_.trim() | ? { $_.InstalledOn -lt (get-date).addyears(-1) } }
```

Just paste them into a here-string and execute this for each of them.
