---
layout: post
title: Can PowerShell Parameters Belong To Multiple Parameter Sets?
date: 2017-06-14 07:00
author: thmsrynr@outlook.com
comments: true
categories: [function design, parameters, PowerShell, powershell]
---
Say you've got a function that takes three parameters: Username, ComputerName and SessionName, but you don't want someone to use ComputerName and SessionName at once. You decide to put them in separate parameter sets. Awesome, except you want Username to be a part of both parameter sets and it doesn't look like you can specify more than one.

This will generate an error:

```
function Do-Thing {
    [CmdletBinding()]
    param (
    [Parameter( ParameterSetName = 'Computer','Session' )][string]$Username,
    [Parameter( ParameterSetName = 'Computer' )][string]$ComputerName,
    [Parameter( ParameterSetName = 'Session' )][PSSession]$SessionName
    )
# Other code
}
```

So how do you make a parameter a member of more than one parameter set? You need more [Parameter()] qualifiers.

<!--more-->

```
function Do-Thing {
    [CmdletBinding()]
    param (
    [Parameter( ParameterSetName = 'Computer' )]
    [Parameter( ParameterSetname = 'Session' )]
    [string]$Username,

    [Parameter( ParameterSetName = 'Computer' )][string]$ComputerName,
    [Parameter( ParameterSetName = 'Session' )][PSSession]$SessionName
    )
# Other code
}
```

They chain together and you now $Username is a part of both parameter sets.
