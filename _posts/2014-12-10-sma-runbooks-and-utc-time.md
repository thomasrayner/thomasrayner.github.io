---
layout: post
title: SMA Runbooks And UTC Time
date: 2014-12-10 02:15
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, PowerShell, powershell, SMA, sma, WMI, wmi]
---
I don't know about you but I hate dealing with systems that use UTC time. I have SMA runbooks that work with Exchange 2013, Exchange Online Protection and other services that annoyingly return results in UTC instead of my local timezone. I wrote an SMA runbook that can be called from other SMA runbooks to do the conversion for me.

<pre class="lang:ps decode:true">workflow ConvertUTCtoLocal
{
    param(
       [parameter(Mandatory=$true)]
       [String] $UTCTime
    )
    $strCurrentTimeZone = (Get-WmiObject win32_timezone).StandardName
    $TZ = [System.TimeZoneInfo]::FindSystemTimeZoneById($strCurrentTimeZone)
    $LocalTime = [System.TimeZoneInfo]::ConvertTimeFromUtc($UTCTime, $TZ)
    Return $LocalTime
}</pre>

It's pretty simple runbook! It has one mandatory parameter $UTCTime which, as the name would suggest, is the UTC time that you want to convert to your local time.

Line 7 gets the local timezone by performing a WMI query. Line 8 uses the [SystemTimeZoneInfo]::FindSystemTimeZoneByID to convert the value returned from the WMI query into a timezone. Line 9 performs the actual conversion from whatever the UTC time is to the timezone determined in line 8.

This whole thing assumes that the time and timezone are set correctly on your SMA runbook servers.
