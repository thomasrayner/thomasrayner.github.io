---
layout: post
title: Use Test-NetConnection in PowerShell to See If A Port Is Open
date: 2017-07-26 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, PowerShell, powershell, remote management, test-netconnection]
---
The days of using <strong>ping.exe</strong> to see if a host is up or down are over. Your network probably shouldn't allow ICMP to just fly around unaddressed, and your hosts probably shouldn't return ICMP echo request (ping) messages either. So how do I know if a host is up or not?

Well, it involves knowing about what your host actually does. What ports are supposed to be open? Once you know that, you can use <strong>Test-NetConnection</strong> in PowerShell to check if the port is open and responding on the host you're interested in.

<!--more-->

<pre class="lang:ps decode:true">PS&gt; Test-NetConnection -ComputerName $computerName -Port 3389


ComputerName     : &lt;snip - name of the computer I'm testing&gt;
RemoteAddress    : &lt;snip - IP address of the computer I'm testing&gt;
RemotePort       : 3389
InterfaceAlias   : Ethernet
SourceAddress    : &lt;snip - my IP address&gt;
TcpTestSucceeded : True</pre>

Here I just checked if port 3389 (for RDP) is open or not. Looks like it is.
