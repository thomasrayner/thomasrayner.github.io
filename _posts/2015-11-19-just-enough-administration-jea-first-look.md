---
layout: post
title: Just Enough Administration (JEA) First Look
date: 2015-11-19 09:37
author: thmsrynr@outlook.com
comments: true
categories: [Automation, JEA, jea, just enough admin, just enough administration, microsoft, mvp, mvp, PowerShell, powershell, PowerShell 5.0, PowerShell ISE, powershell remoting, windows, windows server 2016]
---
If you're reading this, it means that Windows Server 2016 Technical Preview 4 is released (currently available on MSDN) and one of the new features that's available is Just Enough Administration (JEA)! Until now, you could use DSC to play with JEA but now it's baked into Windows Server 2016.

If you're not sure what JEA is or does, check out <a href="https://msdn.microsoft.com/en-us/library/dn896648.aspx" target="_blank">this page published by Microsoft</a>.

<h3>So how do you get started?</h3>

JEA gets put together like a module. There are a bunch of different ways to dive in, but for convenience, I'm just covering this one example. Build on it and learn for yourself how JEA can work for you specifically!

First things first, make a new directory in your modules folder and navigate to it.

```
$dir = 'C:\Windows\system32\WindowsPowerShell\v1.0\Modules\JEA-Test'
new-item -itemtype directory -path $dir
cd $dir
```

So far, so easy. Now, we're going to use the brand new JEA cmdlets to configure what is basically our constrained endpoint.

```
New-PSSessionConfigurationFile -path "$dir\JEA-Test.pssc"
```

This PSSC is the first of two files we're going to make. It's a session config file that specifies the role mappings (we'll get to roles in a second) and some other general config settings. A PSSC file looks like this.

```
@{

# Version number of the schema used for this document
SchemaVersion = '2.0.0.0'

# ID used to uniquely identify this document
GUID = 'c433f896-4241-4b12-b857-059a395c2d2b'

# Author of this document
Author = 'trayner'

# Description of the functionality provided by these settings
# Description = ''

# Session type defaults to apply for this session configuration. Can be 'RestrictedRemoteServer' (recommended), 'Empty', or 'Default'
SessionType = 'RestrictedRemoteServer'

# Directory to place session transcripts for this session configuration
# TranscriptDirectory = 'C:\Transcripts\'

# Whether to run this session configuration as the machine's (virtual) administrator account
# RunAsVirtualAccount = $true

# Groups associated with machine's (virtual) administrator account
# RunAsVirtualAccountGroups = 'Remote Desktop Users', 'Remote Management Users'

# Scripts to run when applied to a session
# ScriptsToProcess = 'C:\ConfigData\InitScript1.ps1', 'C:\ConfigData\InitScript2.ps1'

# User roles (security groups), and the role capabilities that should be applied to them when applied to a session
RoleDefinitions = @{ 'mvp-trayner\test users' = @{ RoleCapabilities = 'testers' } } 

}
```

If you've ever authored a PowerShell module before, this should look familiar. There's only a few things you need to do here. The first is change the value for <em>SessionType</em> to <em>RemoteRestrictedServer. </em>You need to make it this in order to actually restrict the user connections.

You can enable <em>RunAsVirtualAccount</em> if you're on an Active Directory Domain. I won't get too deep into what virtual accounts do because my example is just on a standalone server.

The other important task to do is define the <em>RoleDefinitions</em> line. This is a hashtable where you set a group (in my case, local to my server) assigned to a "RoleCapability". In this case, the role I'm assigning is just named "testers" and the local group on my server is named "test users".

Save that and now it's time to make a new directory. Roles <strong>must</strong> be in a "RoleCapabilities" folder within your module.

```
new-item -itemtype directory "$dir\RoleCapabilities"
```

Now we are going to continue using our awesome new JEA cmdlets to create a PowerShell Role Capabilities file.

```
New-PSRoleCapabilityFile -path "$dir\RoleCapabilities\testers.psrc"
```

<strong>It's very important to note here that the name of my PSRC file is the same as the RoleCapability that I assigned in the PSSC file above.</strong>

PSRC files look like this. Let's point out some of the key areas in this file and some of the tools you now have at your disposal.

Think of a PSRC as a giant white list. If you don't explicitly allow something, it's not going to happen. Because PSRCs all act as white lists, if you have users who are eligible for more than one PSRC (through more than one group membership/role assignment in a PSSC), the access a user gets is everything that's white listed by any role the user is eligible for. That is to say, PSRCs merge if users have more than one that apply.

```
@{

# ID used to uniquely identify this document
GUID = '3e2ca105-db93-4442-acfd-037593c6c644'

# Author of this document
Author = 'trayner'

# Description of the functionality provided by these settings
# Description = ''

# Company associated with this document
CompanyName = 'Unknown'

# Copyright statement for this document
Copyright = '(c) 2015 trayner. All rights reserved.'

# Modules to import when applied to a session
# ModulesToImport = 'MyCustomModule', @{ ModuleName = 'MyCustomModule'; ModuleVersion = '1.0.0.0'; GUID = '4d30d5f0-cb16-4898-812d-f20a6c596bdf' }

# Aliases to make visible when applied to a session
# VisibleAliases = 'Item1', 'Item2'

# Cmdlets to make visible when applied to a session
VisibleCmdlets = 'Get-*', 'Measure-*', 'Select-Object', @{ Name= 'New-Item'; Parameters = @{ Name = 'ItemType'; ValidateSet = 'Directory' }, @{ Name = 'Force' }, @{ Name = 'Path'; ValidateSet = 'C:\Users\testguy\ONLYthis' } }

# Functions to make visible when applied to a session
# VisibleFunctions = 'Invoke-Function1', @{ Name = 'Invoke-Function2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }

# External commands (scripts and applications) to make visible when applied to a session
VisibleExternalCommands = 'c:\scripts\this.ps1'

# Providers to make visible when applied to a session
# VisibleProviders = 'Item1', 'Item2'

# Scripts to run when applied to a session
# ScriptsToProcess = 'C:\ConfigData\InitScript1.ps1', 'C:\ConfigData\InitScript2.ps1'

# Aliases to be defined when applied to a session
#AliasDefinitions = @{ Name = 'test-alias'; Value = 'Get-ChildItem'}

# Functions to define when applied to a session
# FunctionDefinitions = @{ Name = 'MyFunction'; ScriptBlock = { param($MyInput) $MyInput } }

# Variables to define when applied to a session
# VariableDefinitions = @{ Name = 'Variable1'; Value = { 'Dynamic' + 'InitialValue' } }, @{ Name = 'Variable2'; Value = 'StaticInitialValue' }

# Environment variables to define when applied to a session
# EnvironmentVariables = @{ Variable1 = 'Value1'; Variable2 = 'Value2' }

# Type files (.ps1xml) to load when applied to a session
# TypesToProcess = 'C:\ConfigData\MyTypes.ps1xml', 'C:\ConfigData\OtherTypes.ps1xml'

# Format files (.ps1xml) to load when applied to a session
# FormatsToProcess = 'C:\ConfigData\MyFormats.ps1xml', 'C:\ConfigData\OtherFormats.ps1xml'

# Assemblies to load when applied to a session
# AssembliesToLoad = 'System.Web', 'System.OtherAssembly, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'

}
```

Let's skip ahead to line 25. What I'm doing here is white listing any cmdlet that starts with <strong>Get- </strong>or <strong>Measure-</strong> as well as <strong>Select-Object</strong>. Inherently, any of the parameters and values for the parameters are whitelisted, too. I can hear you worrying, though. "What if a Get- command contains a method that allows you to write or set data? I don't want that!" Well, rest assured. JEA runs in <a href="https://technet.microsoft.com/en-us/library/dn433292.aspx" target="_blank">No Language mode</a> which prevents users from doing any of those shenanigans.

Also in line 25, I'm doing something more specific. I'm including a hashtable. Why? Because I want to allow the <strong>New-Item</strong> cmdlet but only certain parameters and values. I'm allowing the ItemType parameter but only if the user sets it to Directory. I'm allowing Force, which doesn't take a value. I'm also allowing the Path attribute, but, only a specific path. If a user tries to use the <strong>New-Item</strong> cmdlet but violates these rules, the user will get an error.

On line 19, I can import specific modules without opening up the <strong>Import-Module</strong> cmdlet. These modules are automatically imported when the session starts.

On line 28, we can make specific functions available to connecting users.

Line 31 is interesting. Here I'm making an individual script available to the connecting user. The script contains a bunch of commands that I haven't white listed, so, is the user going to be able to run it? Yes. Yes they are. The user can run that script and the script will run correctly (assuming other permissions are in place) without having the individual cmdlets white listed. <strong>It is a bad idea to allow your restricted users to write over scripts you make available to them this way. </strong>

On line 37, you can basically configure a login script. Line 40 lets you define custom aliases and line 43 lets you define custom functions that only exist in these sessions. Line 46 is for defining custom variables (like "$myorg = 'ThmsRynr Co.") which can be static or dynamic.

With these tools at your disposal, you can configure absolutely anything about a user's session and experience. Sometimes, you might have to use a little creativity, but anything is possible here.

Lastly, you need to set up the JEA endpoint. You can also overwrite the default endpoint so every connection hits your JEA config but you may want to set up another unconstrained endpoint just for admins... just in case.

```
Register-PSSessionConfiguration -name 'JEA-Test' -path $dir
```

That's it. You're done. Holy, that was way too easy for how powerful it is. Now when a user wants to connect, they just run a command like this and they're in a session limited like you want.

```
Enter-PSSession -ComputerName mvp-trayner -ConfigurationName JEA-Test
```

If they are in my local "Test Users" group, they'll have the "testers" role applied and their session will be constrained like I described above. You'll need to make sure your test users have permissions to remotely connect at all, though, otherwise the connection will be rejected before a JEA config is applied.

<h3>I can think of a bunch of use cases for JEA. For instance...</h3>

<h6>1. Network Admins</h6>

<div>I'd like my network admins to be able to administer DHCP and DNS on our Windows servers which hold these roles without having carte blanche admin rights to everything else. I think this would involve limiting the cmdlets available to those including *DHCP* or *DNS*.</div>

<div></div>

<h6>2. Certificate Management</h6>

<div>We use the <a href="https://pspki.codeplex.com/" target="_blank">PSPKI module</a> for interacting with our Enterprise PKI environment. For this role, I'd deploy the module and give users permissions to use only the PSPKI cmdlets. I'd use the Windows CA permissions/virtual groups to allow or disallow users manage CA, manage certificates, or just request certificates.</div>

<div></div>

<h6>3. Code Promotion</h6>

<div>Allowing people connecting via JEA to read/write only certain areas of a filesystem isn't practical. The way I'd get around this is to allow access to run only one script which performed the copy commands or prompted for additional info as required. You could mix this in with PowerShell Direct and promote code to a server in a DMZ without opening network holes or allowing admin access to a DMZ server.</div>

<div></div>

<h6>4. Service Account for Patching</h6>

<div>We have a series of scripts that apply a set of rules and logic to determine if a server needs to be patched or not. All it needs to do is perform some WMI queries, communicate with SCCM (which has the service installed to actually do the patching) and reboot the server. Instead, right now, that service account has full admin rights on the server.</div>

<div></div>

<h6>5. Help Desk</h6>

<div>Everybody's help desk is different but one job I'd like to send to my help desk is some limited Active Directory management. I'd auto-load the AD module and then give them access to very restricted cmdlets and some parameters. For instance, Get-ADUser and allow -Properties but only allow the memberof, lockedout, enabled and passwordlastset values. I might also allow them to add users to groups but only if the group was in a certain OU or matched a certain string (ie: if the group ends in "distribution list").</div>

<div></div>

<h6>6. Print Operators</h6>

<div>We have a group of staff on-site 24/7 that service a giant high speed print device. There are a number of servers that send it jobs and many are sensitive. I'd like to give the print operators group permissions to reach out and touch these servers only for the purposes of managing print jobs.</div>

<div></div>

<h6>7. Hyper-V Admins/Host Management</h6>

<div>These guys need the Hyper-V module and commands within it as well as some limited rights on the host, like Get WMI/CIM objects but not the ability to set WMI/CIM objects.</div>

<div></div>

<h3>Get playing!</h3>

The possibilities of what you can do with JEA are endless. While the DevOps mentality is flourishing, the need to enable access to different systems is growing. With JEA, you can enable whatever kind of access you need, without enabling a whole bunch of access you don't. That's probably why it's called "Just Enough Administration".
