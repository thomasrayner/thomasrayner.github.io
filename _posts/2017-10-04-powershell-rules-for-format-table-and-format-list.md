---
layout: post
title: PowerShell Rules For Format-Table And Format-List
date: 2017-10-04 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, displaying output, format-list, format-table, outputting data, PowerShell, powershell]
---
In PowerShell, when outputting data to the console, it's typically either organized into a table or a list. You can force output to take either of these forms using the <strong>Format-Table</strong> and the <strong>Format-List</strong> cmdlets, and people who write PowerShell cmdlets and modules can take special steps to make sure their output is formatted as they desire. But, when no developer has specifically asked for a formatted output (for example, by using a .format.ps1xml file to define how an object is formatted), how does PowerShell choose to display a table or a list?

<!--more-->

The answer is actually pretty simple and I'm going to highlight it with an example. Take a look at the following piece of code.

```
PS&gt; get-wmiobject -class win32_operatingsystem | select pscomputername,caption,osarch*,registereduser

PSComputerName  caption                         OSArchitecture registereduser
--------------  -------                         -------------- --------------
workingsysadmin Microsoft Windows 10 Enterprise 64-bit         ThmsRynr@outlook.com
```

I used <strong>Get-WmiObject</strong> to get some information about my operating system. I selected four properties and PowerShell decided to display a table. Now, let's add another property to return.

```
PS&gt; get-wmiobject -class win32_operatingsystem | select pscomputername,caption,osarch*,registereduser,version


PSComputerName : workingsysadmin
caption        : Microsoft Windows 10 Enterprise
OSArchitecture : 64-bit
registereduser : ThmsRynr@outlook.com
version        : 10.0.14393
```

Whoa, now we get a list. What gives?

Well here's how PowerShell decides, by default, whether to display a list or table:

<ul>
    <li>If showing four or fewer properties, show a table</li>
    <li>If showing five or more properties, show a list</li>
</ul>

That's it, that's how PowerShell decides by default whether to show you a list or table.
