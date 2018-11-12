---
layout: post
title: Using PowerShell To Add Groups To "AcceptMessagesOnlyFromDLMembers" Exchange Attribute
date: 2016-06-01 08:00
author: thmsrynr@outlook.com
comments: true
categories: [Automation, Exchange, exchange, PowerShell, powershell]
---
Here's a bit of an obscure task. In Exchange you can configure the <em>AcceptMessagesOnlyFromDLMembers</em> attribute which does what it sounds like it does: it only allows the mail recipient to accept messages from members of specific distribution lists. The problem is, there's no built in method for appending a distribution list (DL) to an existing list of DLs. If you set <em>AcceptMessagesOnlyFromDLMembers</em> equal to a value, it overwrites what was there before. So, I wrote a quick script to append a value instead of overwriting it. You'll need a <a href="http://www.workingsysadmin.com/opening-a-remote-exchange-management-shell/" target="_blank">remote Exchange Management Shell</a> and the AD management module for this.

```
function Add-AcceptMessagesOnlyFromDLMembers 
{
    [CmdletBinding()]
    param (
        [Parameter(Mandatory)]
        [string]$AppendTo,
        [Parameter(Mandatory)]
        [string]$DLName
    )
    
    $arr = $(Get-MailContact $AppendTo | Select-Object AcceptMessagesOnlyFromDLMembers).AcceptMessagesOnlyFromDLMembers
    $arr += ($(Get-ADGroup $NameOfGroup -Properties CanonicalName).CanonicalName)
    set-mailContact $AppendTo -AcceptMessagesOnlyFromDLMembers:"$($arr)"
}
\n```

First things first, I declare the function named <strong>Add-AcceptMessagesOnlyFromDLMembers</strong> which is a bit more verbose than I'd usually like to make it, but I'm also a fan of descriptive function and cmdlet names.

Second, I need some parameters. The mail recipient whose <em>AcceptMessagesOnlyFromDLMembers</em> value we're appending something to, and the DL that we're appending.

Line 11 is where we begin doing the real work. I've got to get the mail contact and select just the value currently in <em>AcceptMessagesOnlyFromDLMembers</em> so I can append something to it. I store that data in <em>$arr</em>.

On line 12, I'm retrieving the <em>CanonicalName</em> attribute for the DL I want to append to the list of DLs that can send mail to this contact. The <em>AcceptMessagesOnlyFromDLMembers</em> attribute is a bit weird in that it only appears to take Canonical Names, not Distinguished names, etc.. I'm appending that value to the end of <em>$arr</em>.

Line 13 is pretty straight forward. I'm setting the <em>AcceptMessagesOnlyFromDLMembers</em> attribute to the value of <em>$arr</em> determined in line 12.

That's it! If this is a task you perform regularly, please take this script and apply it. If you make it more robust, I'd love to see what your modifications are.
