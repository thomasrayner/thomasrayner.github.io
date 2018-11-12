---
layout: post
title: Quick Tip - Which Of These Groups Are These Users Members Of?
date: 2015-09-30 08:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, activedirectory, PowerShell, powershell, PowerShell ISE, powershell ise, quick tip, user management]
---
Here's a quick PowerShell function I put together that you might like to use or pick pieces from. The point of the function is to take a list of usernames and a list of groups and tell you which users are members of which groups, including through nested group membership.

```
#requires -Version 1 -Modules ActiveDirectory
function Test-IsGroupMember
{
    param (
        [Parameter(Mandatory=$True,
                Position=1,
        ValueFromPipeline=$True)]
        [Object]$Usernames,
        [Parameter(Mandatory=$True,
                Position=2,
        ValueFromPipeline=$True)]
        [Object]$Groups
    )

    foreach ($strGroup in $Groups) {
        $arrMembers = @()
        $arrMembers = (Get-ADGroupMember -Identity $strGroup -Recursive).SamAccountName
        Write-Output "$strGroup has $($arrMembers.count) members"
        $Usernames | % { if ($arrMembers -contains $_) { write-host " * $_ is a member of $strGroup" } }
        Write-Output ''
    }
}\n```

As you can see, this function requires the ActiveDirectory PowerShell module and the function is named <strong>Test-IsGroupMember. </strong>It takes two parameters called Usernames and Groups. Both are "object" types so they could be an array or a string. I didn't want to make overloaded versions of a script this simple so I took this shortcut. It's expected that the values in Usernames and Groups will be SamAccountNames.

On Line 15, I start the work. For all of the groups you pass the function, it determines the recursive group members and extracts the SamAccountName attribute of the members returned. Then to the output stream, we write that the currently evaluated group has a number of members. On Line 19, we check to see if any of the usernames in the Usernames parameter are contained within the members of the group. I could have used a <strong>Compare-Object</strong> here but I didn't. If the user is present in both arrays, we report back.

Here are some examples of how I like using this function.

```
#Take an array of users and an array of groups to see which users are in which groups
Test-IsGroupMember @('user1','user2','user3','ThmsRynr') @('Group1','Group2','Group3')

#See if ThmsRynr is a (nested) member of SomeGroup
Test-IsGroupMember ThmsRynr SomeGroup

#See if all the members of InterestingGroup are members of any group whose name matches *Keyword*
Test-IsGroupMember -Usernames (Get-ADGroupMember InterestingGroup).SamAccountName -Groups (Get-ADGroup -filter "Name -like '*Keyword*'").SamAccountName\n```

Pretty flexible.
