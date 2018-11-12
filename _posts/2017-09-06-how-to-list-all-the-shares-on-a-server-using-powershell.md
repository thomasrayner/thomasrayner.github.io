---
layout: post
title: How To List All The Shares On A Server Using PowerShell
date: 2017-09-06 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, fileshare, filesystem, filesystem, PowerShell, powershell, smb, storage]
---
There's a few ways to get all of the shared folders on a server, but not all of them work for all versions of Windows Server. You can use the <strong>Get-SmbShare</strong> cmdlet, or you can make CIM/WMI do the work for you. I'll show you what I prefer, though.

<!--more-->

To use <strong>Get-SmbShare</strong> on a remote computer, you'll create a new CIM session.

<pre class="lang:ps decode:true ">PS&gt; New-CimSession -ComputerName $computername -Credential $creds

Id           : 1
Name         : CimSession1
InstanceId   : 110928f2
ComputerName : computername
Protocol     : WSMAN</pre>

Then you can pass that CIM session to <strong>Get-SmbShare</strong>.

<pre class="lang:ps decode:true ">PS&gt; Get-SmbShare -CimSession $(get-cimsession -id 1)

Name     ScopeName Path                              Description     PSComputerName
----     --------- ----                              -----------     --------------
ADMIN$   *         C:\windows                        Remote Admin    comp
C$       *         C:\                               Default share   comp
D$       *         D:\                               Default share   comp
IPC$     *                                           Remote IPC      comp
print$   *         C:\windows\system32\spool\drivers Printer Drivers comp
Profiles *         D:\Profiles                                       comp
Transfer *         C:\Shares\Transfer                                comp</pre>

But what if the server is (heaven forbid!) older than Windows Server 2012R2? Well, you'd get an error telling you "<em>get-cimclass : The WS-Management service cannot process the request. The CIM namespace win32_share is invalid.</em>". That won't do.

Well, luckily for those older servers, you can use <strong>Get-WmiObject</strong> to retrieve this information.

<pre class="lang:ps decode:true ">PS&gt; Get-WmiObject -Class win32_share -ComputerName $oldComp -Credential $creds


Name         Path                                                  Description
----         ----                                                  -----------
ADMIN$       C:\windows                                            Remote Admin
C$           C:\                                                   Default share
D$           D:\                                                   Default share
IPC$                                                               Remote IPC</pre>

&nbsp;
