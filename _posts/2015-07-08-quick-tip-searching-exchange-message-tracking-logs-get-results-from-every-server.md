---
layout: post
title: Quick Tip - Searching Exchange Message Tracking Logs (Get Results From Every Server)
date: 2015-07-08 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Exchange, exchange, PowerShell, powershell, PowerShell ISE, powershell ise, quick tips]
---
When you use the <strong>Get-MessageTrackingLog</strong> cmdlet, by default, it only searches for messages/events on the server that you're connected to (<a href="http://www.workingsysadmin.com/opening-a-remote-exchange-management-shell/" target="_blank">see my post on creating connections to Exchange</a>). That's not great in a multi-server environment. I want results from every server.

My solution is the following.

<pre class="lang:ps decode:true  ">$results = $null
get-transportservice | foreach-object { $results += Get-MessageTrackingLog -server $_.Name -start (get-date).addhours(-1) -end (get-date) -resultsize unlimited | Select-Object -Property eventid,serverhostname,sender,recipients,messagesubject,timestamp }
$results | Sort-Object -Property Timestamp | ft 
</pre>

The <strong>Get-TransportService</strong> cmdlet gets a list of all the transport servers in your infrastructure. For each of the servers we get back, I'm running the <strong>Get-MessageTrackingLog</strong> cmdlet and appending the results to a $results variable. I'm taking that results collection and sorting it chronologically.
