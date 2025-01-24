---
layout: post
title: PowerShell Function To Get Time Since A User's Password Was Last Changed
date: 2015-09-02 08:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, activedirectory, PowerShell, powershell, PowerShell ISE, powershell ise]
---
Here's a small function I put in my PowerShell profile to tell me how long it's been since an AD user's password was last changed. You do know how to change your PowerShell profile, don't you? Just type the following in a PowerShell prompt.

```
notepad $profile
```

That will open your PowerShell profile in Notepad. You might be asked to create one if you don't have anything there yet. Then just save that and next time you open PowerShell, whatever code you have in your profile will be executed. The code I'm putting in there right now is the definition for this function.

```
function Get-TimeSinceLastPWSet {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory=$True,
        Position=1,
        ValueFromPipeline=$True)]
        [string]$Username
    )
    
    $tsSinceLastPWSet = New-TimeSpan $(get-aduser $Username -Properties Passwordlastset).Passwordlastset $(get-date)
    return $tsSinceLastPWSet
    }
```

It's pretty straight forward. My function is named <strong>Get-TimeSinceLastPWSet</strong> and takes one parameter, the username of the user we're interested in. On Line 10, the actual work gets done. I'm making a new TimeSpan object assigned to <em>$tsSinceLastPWSet</em> which is the time between the user's <em>Passwordlastset</em> AD attribute and the current date/time.

Since the function returns a timespan object, you can manipulate it like this to get more friendly output. (More info on <a href="https://msdn.microsoft.com/en-us/library/txafckwd.aspx?f=255&amp;MSPPError=-2147217396" target="_blank">Composite Formatting from MSDN</a>. No PowerShell examples but it looks a lot like the C#.)

```
Get-TimeSinceLastPWSet ThmsRynr | % { '{0:dd} days, {0:hh} hours' -f $_ }
```

This will give you output that simply looks like "10 days, 12 hours" instead of the generic list formatted output you get when you write out a timespan object. I've actually made that the default behavior of the function I put in my personal profile because that's more valuable to me.

Mine looks like this.

```
function Get-TimeSinceLastPWSet {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory=$True,
                Position=1,
        ValueFromPipeline=$True)]
        [string]$Username
    )
    
    $tsSinceLastPWSet = New-TimeSpan $(get-aduser $Username -Properties Passwordlastset).Passwordlastset $(get-date)
    $strFormatted = '{0:dd} days, {0:hh} hours' -f $tsSinceLastPWSet
    return $strFormatted
    }
```

Just a small tweak. It returns that nice-to-look-at-string instead of the timespan object.
