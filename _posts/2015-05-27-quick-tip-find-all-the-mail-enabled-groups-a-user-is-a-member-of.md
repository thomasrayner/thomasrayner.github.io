---
layout: post
title: Quick Tip - Find All The Mail Enabled Groups A User Is A Member Of
date: 2015-05-27 08:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, Exchange, exchange, PowerShell, powershell, PowerShell ISE, powershell ise, quick tip]
---
Here's a one-liner that will help you find all the mail enabled groups that a user is a member of. A little pre-requisite reading is this bit on group types to understand the difference between a security group and a distribution group: <a title="https://technet.microsoft.com/en-us/library/cc781446%28WS.10%29.aspx?f=255&amp;MSPPError=-2147217396" href="https://technet.microsoft.com/en-us/library/cc781446%28WS.10%29.aspx?f=255&amp;MSPPError=-2147217396" target="_blank">https://technet.microsoft.com/en-us/library/cc781446%28WS.10%29.aspx?f=255&amp;MSPPError=-2147217396</a>

Here's the one-liner!

```
(get-aduser ThmsRynr -properties memberof).memberof | % { get-adgroup $_ } | ? { $_.GroupCategory -eq "Distribution" } | ft Name
```

It might not be the epitome of efficiency but it works and served me well when I needed it to.

First, we're running a <strong>Get-ADUser</strong> command on our interesting user and making sure to retrieve the <em>MemberOf </em>property in addition to the standard properties returned. Out of all of the returned properties, it turns out that <em>MemberOf</em> is the only one I'm interested in so I select only that property by wrapping the command in brackets and appending <em>.MemberOf</em>. Second, I'm piping all of the groups that the user is a member of into a foreach-object loop. For each of the objects returned, I'm performing a <strong>Get-ADGroup</strong>. I have to do this because I can't necessarily tell which groups the user is a member of are mail enabled just from their name, I have to run the <strong>Get-ADGroup</strong> command to get more information. I'm piping these results into a where-object command where I select only the groups whose <em>GroupCategory</em> is equal to "Distribution" (see the pre-requisite reading above). Then I format the group names into a table.

I could have got every group in my Active Directory and searched for groups that contained my user as a member and were Distribution types, but in my situation, it was faster to only spot check the groups that the user was actually a member of. I have a lot of groups, you might not.
