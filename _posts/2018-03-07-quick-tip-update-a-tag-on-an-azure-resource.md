---
layout: post
title: Quick Tip - Update a Tag on an Azure Resource
date: 2018-03-07 07:30
author: thmsrynr
comments: true
categories: [Automation, automation, Azure, azure, DevOps, devops, PowerShell, powershell]
---
Working with Azure resources can be a bit of an adventure sometimes. Say you want to update a tag on an Azure resource. Not remove it, but change its value. If you try to add a tag with the same name but different value, you'll get an error that the tag already exists. Some of the ways you have available to get rid of a tag involve dropping all the other tags assigned to a resource. So, what do you do?

In this example, I have a couple VMs with a tag named "user" and a value of "thmsrynr", and I want to keep the tag but change the value to "Thomas".

<!--more-->

Well, this extravagant one-liner will do the trick.
```
Find-AzureRmResource -TagName user | 
    ForEach-Object { Get-AzureRmResource -ResourceId $_.ResourceId |
    ForEach-Object { $tags = $_.Tags; 
                     $tags['user'] = 'Thomas'; 
                     Set-AzureRmResource -Tag $tags -ResourceId $_.ResourceId } }
```
I like Find-AzureRmResource best for searching for resources with a specific tag, but it doesn’t return the tags for some reason that is beyond me. You can search by tag but the tags aren’t returned? Weird, right?

Anyway, I pipe everything I find into Get-AzureRmResource which is bad at searching for resources but DOES return the tags. Then for the resource I find, I store the tags on that resource in a temporary variable (named <strong>$tags</strong>), and then I work with the variable instead of working directly with the Azure object to update the “user” tag I care about. Then I set the tags on that resource to be what I stored. This should keep all the other tags intact, and update the value of one specific tag.

You could, and probably should, expand this into a more flexible function with parameters and filtering and such, but this example shows you how the tricky bits work.
