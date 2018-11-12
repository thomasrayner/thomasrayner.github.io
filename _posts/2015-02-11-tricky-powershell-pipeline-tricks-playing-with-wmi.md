---
layout: post
title: Tricky PowerShell Pipeline Tricks - Playing With WMI
date: 2015-02-11 08:30
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, PowerShell ISE, powershell ise, WMI, wmi]
---
Here's a quick task: Get the WMI object <em>win32_bios</em> for a computer.<em> </em>Using PowerShell, that's really easy. You just run <strong>Get-WMIObject win32_bios</strong>. Now what if you wanted all the extended properties of the object (not just the five that it normally returns) and ONLY to return the properties that actually have a value assigned?

Well this question just got trickier. <em>win32_bios</em> isn't very big so it's an easy one to play with in this example. Let's step through a couple commands so we know what we're dealing with.

<pre class="lang:ps decode:true ">Get-WMIObject win32_bios


SMBIOSBIOSVersion : 6.00
Manufacturer      : Phoenix Technologies LTD
Name              : PhoenixBIOS 4.0 Release 6.0     
SerialNumber      : VMware-42 00 a6 a6 02 95 ec 5e-89 05 0a cd b1 3b aa c6
Version           : INTEL  - 6040000</pre>

Well okay, there are the five properties that we knew the command returns by default. We know the extended properties are in there and we can prove it.

<pre class="lang:ps decode:true ">Get-WMIObject win32_bios | Select-Object -Property *


PSComputerName        : workingsysadmin
Status                : OK
Name                  : PhoenixBIOS 4.0 Release 6.0     
Caption               : PhoenixBIOS 4.0 Release 6.0     
SMBIOSPresent         : True
__GENUS               : 2
__CLASS               : Win32_BIOS
__SUPERCLASS          : CIM_BIOSElement
__DYNASTY             : CIM_ManagedSystemElement
__RELPATH             : Win32_BIOS.Name="PhoenixBIOS 4.0 Release 6.0     ",SoftwareElementID="PhoenixBIOS 4.0 Release 6.0     ",SoftwareElementState=3,TargetOperatingSystem=0,Version="INTEL  - 6040000"
__PROPERTY_COUNT      : 27
__DERIVATION          : {CIM_BIOSElement, CIM_SoftwareElement, CIM_LogicalElement, CIM_ManagedSystemElement}
__SERVER              : workingsysadmin
__NAMESPACE           : root\cimv2
__PATH                : \\workingsysadmin\root\cimv2:Win32_BIOS.Name="PhoenixBIOS 4.0 Release 6.0     ",SoftwareElementID="PhoenixBIOS 4.0 Release 6.0     ",SoftwareElementState=3,TargetOperatingSystem=0,Version="INTEL  - 6040000"
BiosCharacteristics   : {4, 7, 8, 9...}
BIOSVersion           : {INTEL  - 6040000, PhoenixBIOS 4.0 Release 6.0     }
BuildNumber           : 
CodeSet               : 
CurrentLanguage       : 
Description           : PhoenixBIOS 4.0 Release 6.0     
IdentificationCode    : 
InstallableLanguages  : 
InstallDate           : 
LanguageEdition       : 
ListOfLanguages       : 
Manufacturer          : Phoenix Technologies LTD
OtherTargetOS         : 
PrimaryBIOS           : True
ReleaseDate           : 20110921000000.000000+000
SerialNumber          : VMware-42 00 a6 a6 02 95 ec 5e-89 05 0a cd b1 3b aa c6
SMBIOSBIOSVersion     : 6.00
SMBIOSMajorVersion    : 2
SMBIOSMinorVersion    : 4
SoftwareElementID     : PhoenixBIOS 4.0 Release 6.0     
SoftwareElementState  : 3
TargetOperatingSystem : 0
Version               : INTEL  - 6040000
Scope                 : System.Management.ManagementScope
Path                  : \\workingsysadmin\root\cimv2:Win32_BIOS.Name="PhoenixBIOS 4.0 Release 6.0     ",SoftwareElementID="PhoenixBIOS 4.0 Release 6.0     ",SoftwareElementState=3,TargetOperatingSystem=0,Version="INTEL  - 6040000"
Options               : System.Management.ObjectGetOptions
ClassPath             : \\workingsysadmin\root\cimv2:Win32_BIOS
Properties            : {BiosCharacteristics, BIOSVersion, BuildNumber, Caption...}
SystemProperties      : {__GENUS, __CLASS, __SUPERCLASS, __DYNASTY...}
Qualifiers            : {dynamic, Locale, provider, UUID}
Site                  : 
Container             :</pre>

There's everything! That's a lot of blanks, though. Depending on the type of reporting you're doing, that might not be so nice to look at. I know that I'd like to get them out. Luckily with PowerShell 4.0, it's really easy if you use the <a title="Pipeline Variables" href="https://technet.microsoft.com/en-us/library/hh847884.aspx" target="_blank"><strong>-PipelineVariable</strong> parameter</a>.

<pre class="lang:ps decode:true  ">Get-WmiObject win32_bios -PipelineVariable bios | 
  foreach {
   $props = $_.psobject.properties.name | Where-Object {$bios.$_}
   $bios | select $props
  }</pre>

I've left out the output since it's every property that has a value and none of the ones that have a blank. Let's take a look at what's actually happening here.

On Line 1, we're running the same command we ran the last two times except we assigned a Pipeline Variable which will be named $bios (you omit the $ when assigning the name of the variable). We enter a foreach loop on Line 2.

On Line 3, we're setting the value of $props and on Line 4, we're writing out the part of the WMI object that contains it. The tricky thing here is how we get the value of $props. Look at how we use the Pipeline Variable and the <em>.PSObject.Properties.Name</em> property to identify the items with a value.

<h2>Well that's great but what if I don't have PowerShell 4.0 or found that example really confusing?</h2>

Don't worry, this is pretty easy to do in earlier versions of PowerShell, too.

<pre class="lang:ps decode:true">gwmi win32_bios | %{$wmi = $_}
Select-Object -inputobject $wmi -property ($wmi.Properties.Name | Where-Object -FilterScript {$wmi.item($_)})</pre>

I started using some more shortcuts (gmi and % instead of Get-WMIObject and foreach).

In Line 1, I'm doing the same ol' <strong>Get-WMIObject</strong> command that I did before and in down the pipe, I'm assigning the value to $wmi. I could have also done "<strong>$wmi = gmi win32_bios</strong>" but this strategy has benefits if you're planning on scaling this script out.

In Line 2, I'm doing some tricky <strong>Select-Object</strong> work. The input for the command is $wmi, which isn't so tricky, but the property that we're selecting <em>is</em> pretty tricky. <strong>-Property</strong> takes an array, so we can put a command in there as long as it returns an array.

$wmi has a property of .Properties.Name which is an array of all the names of the properties attached to the WMI object that got returned in Line 1 (that we are using as our input). We don't just want all the properties, though, so we need to select only the ones with a value (not null). We do that by piping the list of all the properties into a <strong>Where-Object</strong> command.

The <strong>Where-Object</strong> command has a tricky property called <strong>-FilterScript</strong> which basically acts as an implicit IF statement. If you wrote <strong>Where-Object -FilterScript {$true} </strong>then you would return every object in the pipe. If you wrote <strong>Where-Object -FilterScript {($num = $((Get-Random -Minimum 1 -Maximum 100) % 2) -eq 1)} </strong>you would get random properties because sometimes the statement will be true and sometimes the statement will be false. These are all silly items to filter on, though.

In my script, I'm filtering on if the current property the script is looking at has a value in $wmi. If the property is 0 or null and therefore doesn't exist, <strong>$wmi.item($_)</strong> will return false and that line won't be returned. It's basically a test to see if there's a string or not. Consider this example:

<pre class="lang:ps decode:true">$var1 = [string]$null
$var2 = "something"

if ($var1) { write-host "Var1 has a value" } else { write-host "Var1 has no value" }
if ($var2) { write-host "Var2 has a value" } else { write-host "Var1 has no value" }

#Will return
#Var1 has no value
#Var2 has a value</pre>

Because $var1 doesn't have an actual value assigned to it, an <strong>if ($var1) </strong>will return false. That's the same logic we are using all throughout the above code.

Tricky, right?
