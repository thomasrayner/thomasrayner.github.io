---
layout: post
title: Quick Tip - Search Remote Computer Certificate Store
date: 2015-04-29 07:30
author: thmsrynr@outlook.com
comments: true
categories: [certificates, PKI, pki, PowerShell, powershell, PowerShell ISE, powershell ise, quick tip]
---
It's really easy to search your local certificate store using PowerShell. You simply run a command like this.

<pre class="lang:ps decode:true ">dir Cert:\LocalMachine -rec | ? { $_.Subject -match "Interesting" }</pre>

The above command will recursively look through all the certs in the local machine store and return the ones that have the word "Interesting" in the subject. Not exactly re-inventing the wheel here.

There's not a ton of great options for snooping through the certificate store of remote computers, though. The solution I chose to get around this is dead simple. I used the <strong>Invoke-Command</strong> cmdlet to scan the certificate store of a remote computer. It's so easy that it almost feels like cheating.

<pre class="lang:ps decode:true ">Invoke-Command -ScriptBlock { dir Cert:\LocalMachine -rec | ? { $_.Subject -match "Interesting" } } -ComputerName ThmsRynr.mydomain.tld</pre>

&nbsp;
