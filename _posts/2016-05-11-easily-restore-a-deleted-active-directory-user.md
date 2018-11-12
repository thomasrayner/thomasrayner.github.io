---
layout: post
title: Easily Restore A Deleted Active Directory User
date: 2016-05-11 08:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, activedirectory, PowerShell, powershell, recycle bin]
---
If you have a modern version of Active Directory, you have the opportunity to enable the Active Directory Recycle Bin. Once enabled, you have a chance to recover a deleted item once it has been removed from Active Directory.

Here's a quick and easy script to recover a user based on their username.

```
$dn = (Get-ADObject -SearchBase (get-addomain).deletedobjectscontainer -IncludeDeletedObjects -filter "samaccountname -eq '$Username'").distinguishedname
Restore-ADObject -identity $dn
```

On the first line, we're getting the DistinguishedName for the deleted user. The DN changes when a user gets deleted because it's in the Recycle Bin now. Where's your deleted objects container? Well it's easily found with the <strong>(Get-ADDomain).DeletedObjectsContainer</strong> part of line 1. All we're doing is searching for AD objects in the deleted objects container whose username matches the one we're looking for. We need to make sure the <strong>-IncludeDeletedObjects</strong> flag is set or nothing that's deleted will be returned.

On the second line, we're just using the <strong>Restore-ADObject</strong> cmdlet to restore the object at the DN we found above.
