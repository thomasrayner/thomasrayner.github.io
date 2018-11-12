---
layout: post
title: Quick Tip - Protect Your Active Directory From Finger Slips
date: 2015-04-15 08:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, PowerShell, powershell, PowerShell ISE, powershell ise, quick tip]
---
Do you ever worry about giving Domain Admin or other Active Directory privileges to people? I do, so I decided to protect some sensitive items in my AD from accidental deletion - or as I like to call it, protecting against finger slips.

[caption id="attachment_164" align="aligncenter" width="403"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/03/3-16-2015-10-47-03-AM.png"><img class="wp-image-164 size-full" src="http://www.workingsysadmin.com/wp-content/uploads/2015/03/3-16-2015-10-47-03-AM.png" alt="3-16-2015 10-47-03 AM" width="403" height="482" /></a> We're talking about this flag.[/caption]

I've got some OUs that have user and group objects that I would really miss if they were to be accidentally deleted. Furthermore, I would really miss any entire OU if it were to be deleted. I'm not interested in protecting individual computer accounts or user/group accounts in non-sensitive OUs.

Here's the script I used:

```
$arrOUs = @("Sensitive OU1","Sensitive OU2")
$arrOUs | % { Get-ADObject -SearchBase "OU=$($_),DC=sub,DC=domain,DC=tld" -filter {(ObjectClass -eq "group")} | Set-ADObject -ProtectedFromAccidentalDeletion:$true }
$arrOUs | % { Get-ADObject -SearchBase  "OU=$($_),DC=sub,DC=domain,DC=tld" -filter {(ObjectClass -eq "user")} | Set-ADObject -ProtectedFromAccidentalDeletion:$true }
Get-ADOrganizationalUnit -filter * | Set-ADObject -ProtectedFromAccidentalDeletion:$true
```

Line 1 defines an array of names of my sensitive OUs. Lines 2 and 3 are basically the same: they get all the AD objects in the sensitive OUs with an ObjectClass of group or user and protect them from accidental deletion. Why do this in two lines? I was getting inconsistent results (computer and other objects were returned) when I tried combining the filter. My AD isn't that big so this works just fine for me. Line 4 protects all my OUs in my AD from accidental deletion.
