---
layout: post
title: Connecting to Exchange Online Using Multi-Factor Authentication via PowerShell
date: 2017-06-07 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Exchange, exchange, mfa, multi-factor authentication, PowerShell, powershell]
---
Using PowerShell to manage your Microsoft cloud services like Exchange Online is awesome. Using multi-factor authentication (MFA) is also awesome. For some reason, using the two together is not awesome. Many of the Microsoft docs on this seem to suggest you just perform all your administrative tasks from a shell that you launch entirely separately from a normal PowerShell console. I would rather be able to connect to Exchange Online using MFA via PowerShell through a normal console, or as part of another tool. Let me show you how.

<!--more-->

The first thing you'll need to do is <a href="https://technet.microsoft.com/en-us/library/mt775114(v=exchg.160).aspx" target="_blank" rel="noopener noreferrer">install the tool at this page</a>. This will give you all the tools and libraries you need to install to connect to Exchange Online using MFA via PowerShell, including that special, magic console. Now that you have the tools installed, you can use this snippet to connect from a normal PowerShell console or from within another PowerShell-based tool.
```
$modules = @(Get-ChildItem -Path "$($env:LOCALAPPDATA)\Apps\2.0" -Filter "Microsoft.Exchange.Management.ExoPowershellModule.manifest" -Recurse )
$moduleName =  Join-Path $modules[0].Directory.FullName "Microsoft.Exchange.Management.ExoPowershellModule.dll"
Import-Module -FullyQualifiedName $moduleName -Force
$scriptName =  Join-Path $modules[0].Directory.FullName "CreateExoPSSession.ps1"
. $scriptName
$null = Connect-EXOPSSession
$exchangeOnlineSession = (Get-PSSession | Where-Object { ($_.ConfigurationName -eq 'Microsoft.Exchange') -and ($_.State -eq 'Opened') })[0]
```
On lines 1 and 2, I'm getting the location of the different tools and libraries that we installed earlier. Once I find the ExoPowerShellModule.dll, I can import it like any other module, except I'm specifying the full path, on line 3.

Lines 4 and 5 are where I find and dot source CreateExoPSSession.ps1 which is the script that contains the <strong>Connect-EXOPSSession</strong> cmdlet (which I'd be remiss if I didn't mention violates the PowerShell naming standards created by the community and advertised by Microsoft). That cmdlet will trigger a login process that includes MFA, similar to how <strong>Login-AzureRmAccount</strong> works.

Finally on lines 6 and 7, I'm creating a new session and then assigning it to a variable called $exchangeOnlineSession. Then I can import that session and I'll be away to the races.

It's not as convenient or straightforward as connecting without MFA, but it's definitely safer.
