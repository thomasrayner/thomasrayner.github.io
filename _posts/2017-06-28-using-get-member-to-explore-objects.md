---
layout: post
title: Using Get-Member to Explore Objects
date: 2017-06-28 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, get-member, PowerShell, powershell, Uncategorized, working with objects]
---
Last week, I put out a post about<a href="http://www.workingsysadmin.com/using-select-object-to-explore-objects/" target="_blank" rel="noopener noreferrer"> using Select-Object to explore PowerShell objects</a>. This week, I am going to quickly cover using <strong>Get-Member</strong> to do the same.

<!--more-->

Let's say you're using <strong>Get-CimInstance</strong> to get information about the operating system. You might do something like this.

```
PS&gt; Get-CimInstance -ClassName win32_operatingsystem

SystemDirectory     Organization          BuildNumber RegisteredUser        SerialNumber            Version
---------------     ------------          ----------- --------------        ------------            -------
C:\windows\system32 &lt;snip&gt;                14393       &lt;snip&gt;                &lt;snip&gt;                  10.0.14393
```

As is the case with our example last week, there's more stuff returned and available to us than what is returned by default. Let's use <strong>Get-Member</strong> to see what it all is.

```
PS&gt; Get-CimInstance -ClassName win32_operatingsystem | get-member


   TypeName: Microsoft.Management.Infrastructure.CimInstance#root/cimv2/Win32_OperatingSystem

Name                                      MemberType  Definition
----                                      ----------  ----------
Clone                                     Method      System.Object ICloneable.Clone()
Dispose                                   Method      void Dispose(), void IDisposable.Dispose()
Equals                                    Method      bool Equals(System.Object obj)
GetCimSessionComputerName                 Method      string GetCimSessionComputerName()
GetCimSessionInstanceId                   Method      guid GetCimSessionInstanceId()
GetHashCode                               Method      int GetHashCode()
GetObjectData                             Method      void GetObjectData(System.Runtime.Serialization.SerializationInfo info, System.Runtime.Serialization.StreamingCon... GetType                                   Method      type GetType()
ToString                                  Method      string ToString()
BootDevice                                Property    string BootDevice {get;}
BuildNumber                               Property    string BuildNumber {get;}
BuildType                                 Property    string BuildType {get;}
Caption                                   Property    string Caption {get;}
CodeSet                                   Property    string CodeSet {get;}
CountryCode                               Property    string CountryCode {get;}
CreationClassName                         Property    string CreationClassName {get;}
CSCreationClassName                       Property    string CSCreationClassName {get;}
CSDVersion                                Property    string CSDVersion {get;}
CSName                                    Property    string CSName {get;}
CurrentTimeZone                           Property    int16 CurrentTimeZone {get;}
DataExecutionPrevention_32BitApplications Property    bool DataExecutionPrevention_32BitApplications {get;}
DataExecutionPrevention_Available         Property    bool DataExecutionPrevention_Available {get;}
DataExecutionPrevention_Drivers           Property    bool DataExecutionPrevention_Drivers {get;}
DataExecutionPrevention_SupportPolicy     Property    byte DataExecutionPrevention_SupportPolicy {get;}
Debug                                     Property    bool Debug {get;}
Description                               Property    string Description {get;set;}
Distributed                               Property    bool Distributed {get;}
&lt;output truncated&gt;
```

Holy smokes, there's a lot of stuff there. As with <strong>Select-Object</strong>, you can see all the different properties that exist in this object. The big difference here is that you can see all the different methods this object comes with, too. You could store this information in a variable and then invoke the <strong>.HashCode</strong><strong>()</strong> on it and see the output of that, like this.

```
PS&gt; $osInfo = Get-CimInstance -ClassName win32_operatingsystem

PS&gt; $osInfo.GetHashCode()
57422975
```

There's a lot of examples of methods that are more interesting than this, but you can play with it and make this work for you.

&nbsp;
