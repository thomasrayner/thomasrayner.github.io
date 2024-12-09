---
layout: post
title: Get All The Members Of The Distributions Lists That A User Is A Member Of
date: 2015-12-16 08:30
author: thmsrynr@outlook.com
comments: true
categories: [distribution groups, Exchange, exchange, PowerShell, powershell, PowerShell ISE, powershell ise]
---
This is kind of a weird script tip but I bumped into a need for this kind of script so I thought I'd share it. In this post, I have a user and I want to get all the members of all the distribution lists that the user is a member of. That is to say, if the user is a member of DL1, DL2 and DL3 distribution lists, I want to get all the other members of all those distribution lists. You're going to need <a href="http://www.workingsysadmin.com/opening-a-remote-exchange-management-shell/" target="_blank">a remote Exchange shell</a> for this.

Here's the code I came up with.

```
$DN = 'CN=ThmsRynr,OU=BestUsers,DC=lab,DC=workingsysadmin,DC=com'
Get-DistributionGroup -filter "members -eq '$DN'" | Select-Object Name,@{l='Members';e={(Get-DistributionGroupMember $_.SamAccountName -ResultSize Unlimited | % { $_.Name }) -join '; ' }}
```

Line 1 is just declaring a variable to hold the DistinguishedName attribute for the user I am interested in. Line 2 is the work line. The first thing I'm doing is getting all the distribution groups which have a member equal to the DN of the user I'm interested in. Now, the weirdness happens...

When you do a <strong>Get-DistributionGroup</strong>, you do not get the members of that group back with it. Here are the properties that come back that contain the string "mem" in the name.

```
PS C:\&gt; Get-DistributionGroup -filter "members -eq '$DN'" | Select-Object -First 1 | Get-Member | Where-Object Name -match 'mem' | Select-Object Name

Name
----
AcceptMessagesOnlyFromDLMembers
AcceptMessagesOnlyFromSendersOrMembers
AddressListMembership
BypassModerationFromSendersOrMembers
MemberDepartRestriction
MemberJoinRestriction
RejectMessagesFromDLMembers
RejectMessagesFromSendersOrMembers
```

Nothing in there contains the members. So back to the command I wrote to accomplish my goal.

I'm piping the Distribution Groups returned into a <strong>Select-Object</strong> cmdlet to return the Name property and then a custom column. The label is Members and the content is going to just be a string of all the Distribution Group members' names separated by semicolons. The expression for my custom column is a <strong>Get-DistributionGroupMember</strong> command for the Distribution Group piped into a <strong>Foreach-Object</strong> (alias is "%") which returns an array of all the names of the members in the Distribution Group. I use the <strong>-join</strong> command to take the array and convert it into a string separated by semicolons.

It's just that easy!
