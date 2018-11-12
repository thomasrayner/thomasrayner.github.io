---
layout: post
title: Using Select-Object to Explore Objects
date: 2017-06-21 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, PowerShell, powershell, select-object, working with objects]
---
When you're first getting started with PowerShell, you may not be aware that sometimes when you run a command to get data, the information returned to the screen is not ALL the information that the command actually returned.

<!--more-->

Let me clarify with an example. If you run the <strong>Get-ChildItem</strong> cmdlet, you'll get a bit of information back about all the files in whichever directory you specified.

```
PS&gt; Get-ChildItem c:\temp\demo


    Directory: C:\temp\demo


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         6/5/2017   8:11 AM              0 thing.txt\n```

This is not all the data that got returned, though. There are far more properties than just Mode, LastWriteTime, Length and Name to be examined. What are they? Well, we can pipe this cmdlet into <strong>Select-Object -Property *</strong> to see them.

```
PS&gt; Get-ChildItem c:\temp\demo | Select-Object -Property *


PSPath            : Microsoft.PowerShell.Core\FileSystem::C:\temp\demo\thing.txt
PSParentPath      : Microsoft.PowerShell.Core\FileSystem::C:\temp\demo
PSChildName       : thing.txt
PSDrive           : C
PSProvider        : Microsoft.PowerShell.Core\FileSystem
PSIsContainer     : False
Mode              : -a----
VersionInfo       : File:             C:\temp\demo\thing.txt
                    InternalName:
                    OriginalFilename:
                    FileVersion:
                    FileDescription:
                    Product:
                    ProductVersion:
                    Debug:            False
                    Patched:          False
                    PreRelease:       False
                    PrivateBuild:     False
                    SpecialBuild:     False
                    Language:

BaseName          : thing
Target            : {}
LinkType          :
Name              : thing.txt
Length            : 0
DirectoryName     : C:\temp\demo
Directory         : C:\temp\demo
IsReadOnly        : False
Exists            : True
FullName          : C:\temp\demo\thing.txt
Extension         : .txt
CreationTime      : 6/5/2017 8:11:04 AM
CreationTimeUtc   : 6/5/2017 2:11:04 PM
LastAccessTime    : 6/5/2017 8:11:04 AM
LastAccessTimeUtc : 6/5/2017 2:11:04 PM
LastWriteTime     : 6/5/2017 8:11:04 AM
LastWriteTimeUtc  : 6/5/2017 2:11:04 PM
Attributes        : Archive\n```

Look at all that goodness. You can select specific properties by replacing the star with the names of the properties you want to see.

```
PS&gt; Get-ChildItem c:\temp\demo | Select-Object -Property Name, Attributes, IsReadOnly

Name      Attributes IsReadOnly
----      ---------- ----------
thing.txt    Archive      False\n```

Happy scripting!
