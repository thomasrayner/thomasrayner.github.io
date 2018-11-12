---
layout: post
title: How Do You Tell If Two Directories Have The Same Permissions?
date: 2015-07-22 08:30
author: thmsrynr@outlook.com
comments: true
categories: [acl, file system, permissions, PowerShell, powershell, PowerShell ISE, powershell ise]
---
The title of this post is a bit funny. The answer is obviously "You can pop both folders open in Windows Explorer, right click, Properties and compare the security tab!" right? Well, you can, but what about folders that have a lot of complicated permissions? What if you want to compare 100 folders? I don't know about you but I'm not opening 100 folders and comparing the permissions on them all manually. <em>If only PowerShell could help us!</em> Well it can.

In this example, I have three subdirectories in my c:\temp folder. They're named test1, test2 and test3. Test1 and test2 have the same permissions but test3 has different permissions than the first two.

The first command to get familiar with is the <strong>Get-ACL</strong> command. ACL stands for Access Control List. This command may take different objects as parameters but one type of object is a path to a directory. Do a <strong>Get-ACL <em>someDirectory</em> | Get-Member</strong> and you'll see the huge number of methods and properties that get returned. We're only really interested in one property though, the <em>Access</em> property.

```
(Get-Acl c:\temp\test1).Access

#returns
FileSystemRights  : FullControl
AccessControlType : Allow
IdentityReference : BUILTIN\Administrators
IsInherited       : True
InheritanceFlags  : ContainerInherit, ObjectInherit
PropagationFlags  : None

FileSystemRights  : FullControl
AccessControlType : Allow
IdentityReference : NT AUTHORITY\SYSTEM
IsInherited       : True
InheritanceFlags  : ContainerInherit, ObjectInherit
PropagationFlags  : None

FileSystemRights  : ReadAndExecute, Synchronize
AccessControlType : Allow
IdentityReference : BUILTIN\Users
IsInherited       : True
InheritanceFlags  : ContainerInherit, ObjectInherit
PropagationFlags  : None

FileSystemRights  : Modify, Synchronize
AccessControlType : Allow
IdentityReference : NT AUTHORITY\Authenticated Users
IsInherited       : True
InheritanceFlags  : None
PropagationFlags  : None
```

Look at that. A list of all the different permissions on the folder we care about! Now all we have to do is compare this ACL to the ACLs of other directories. For this, why not simply use the <strong>Compare-Object</strong> cmdlet? Here's the full script to compare three folders and commands. I'll break it all down.

```
$ACLone = get-acl "C:\temp\test1"
$ACLtwo = get-acl "C:\temp\test2"
$ACLthree = get-acl "C:\temp\test3"
write-host "Compare 1 and 2 ----------------------"
Compare-Object -referenceobject $ACLone -differenceobject $ACLtwo -Property access | select sideindicator -ExpandProperty access | ft
write-host "Compare 1 and 3 ----------------------"
Compare-Object -referenceobject $ACLone -differenceobject $ACLthree -Property access | select sideindicator -ExpandProperty access | ft
```

The first three lines are just getting the ACLs for the three directories I care about and storing the values in variables. There's tons of better ways to get and organize that information but this way lays it out nicely for this example.

Line 5 is our first <strong>Compare-Object</strong> command and it's actually pretty intuitive, in my opinion. It's taking a reference object ($ACLone) and comparing to a difference object ($ACLtwo) and it's comparing the <em>Access</em> property. This will return the differences between the two ACLs which is totally our goal. The problem is it looks kind of ugly and useless so I pipe the result into a select command. I'm expanding the <em>Access</em> property so you can see exactly which items are different and formatting it as a table.

On lines 5 and 7 you'll see I'm also selecting a property called <em>SideIndicator</em>. What's that? Well, when you compare two objects, in addition to seeing a list of differences, don't you also want to see which object has the different values? <em>SideIndicator</em> is either <strong>=&gt; </strong>or <strong>&lt;=</strong> depending on which object has the unique value. I'll explain.

Here is the output of line 7 (comparing two directories with different ACLs). It's snipped and edited but you'll see the important parts and yours won't look too different.

[caption id="attachment_179" align="aligncenter" width="989"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/05/4-6-2015-1-35-28-PM.png" target="_blank"><img class="  wp-image-179 size-full" src="http://www.workingsysadmin.com/wp-content/uploads/2015/05/4-6-2015-1-35-28-PM.png" alt="4-6-2015 1-35-28 PM" width="989" height="169" /></a> Click for larger[/caption]

The side indicator column points left or right. This indicates whether the unique value is on the reference object or the difference object. Arrows pointing left indicate items on the reference object only, arrows pointing to the right indicate items on the difference object only.

There you go! You can use this and scale it to programatically compare file system permissions using PowerShell.

<a href="https://gallery.technet.microsoft.com/scriptcenter/Compare-Permissions-Of-Two-82c95961" target="_blank">You can download a script I published for this purpose from the TechNet Script Center.</a>
