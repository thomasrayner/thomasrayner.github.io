---
layout: post
title: Quick Script Share - Tell Me Everyone With Access To This Directory
date: 2015-09-16 08:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, isesteroids, PowerShell, powershell, PowerShell ISE, powershell ise, quick script sharing, quick tip]
---
Trying something new. Here's a quick script I threw together to satisfy a request along the lines of "tell me all the users who have access to this directory". It’s easy to see all the groups that have access just by right-clicking a directory and going to the Security tab but it’s a pain to get all the users who belong to those groups – especially if there are nested groups (within nested groups, within nested groups). Hence, this script. In addition to the ActiveDirectory PowerShell module, you of course need to be able to read the ACL on the directory you are interested in so use your admin account.

In this experimental post, I'm not going to break down the script, but instead, I've quickly commented in-line most of the tricky bits. I think it's pretty straight forward, but, I wrote it. Let me know what you think.

```
#requires -Version 1 -Modules ActiveDirectory

#function to return the SamAccountNames of all the users in a group - if the group is empty, return the name of the group
Function Get-NestedGroupMember {
    param
    (
        [Parameter(Mandatory=$True,
                Position=1,
        ValueFromPipeline=$True)]
        [string]$Group
    )
 
    $Users = @(Get-ADGroupMember $group -recursive).SamAccountName
    if ($Users) { return $Users }
    else { return $Group }
} 

#function to enumerate types of access held by individuals to a directory
Function Get-Access {
    param
    (
        [Parameter(Mandatory=$True,
                Position=1,
        ValueFromPipeline=$True)]
        [string]$Dir
    )
    
    #record the current erroractionpreference so we can set it back later
    $OldEAP = $ErrorActionPreference
    
    #set erroracctionpreference to silently continue so we ignore errors from empty groups and weird broken ACLs
    $ErrorActionPreference = 'silentlycontinue'
    
    #get the full ACL of the directory from the parameter
    $ACL = Get-Acl $Dir
    
    #retrieve the Access attribute
    $arrAccess = @($ACL.Access)
    
    #separate the IdentityReference and FileSystemRights attributes from within the Access attribute
    $arrIdentRef = $arrAccess | select-object IdentityReference, FileSystemRights
    
    #for each item in the access attribute of the ACL, write the type of filesystemrights associated with the entry and get the recursive group membership
    $arrIdentRef | % { Write-Output "ACCESS $($_.FileSystemRights) HELD BY: `r`n$(Get-NestedGroupMember $_.IdentityReference.Value.ToString().Split('\')[-1])"; Write-Output "`r`n`r`n" }
    
    #set the erroractionpreference back to whatever it was before we started
    $ErrorActionPreference = $OldEAP
}

Get-Access '\\host\share\some folder'
```

&nbsp;
