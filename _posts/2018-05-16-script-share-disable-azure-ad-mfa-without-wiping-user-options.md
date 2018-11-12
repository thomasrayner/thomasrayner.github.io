---
layout: post
title: Script Share: Disable Azure AD MFA Without Wiping User Options
date: 2018-05-16 07:30
author: thmsrynr
comments: true
categories: [active directory, Automation, Azure, conditional access, DevOps, mfa, msol, msonline, PowerShell, powershell, user management]
---
How's this for a niche topic? If you want to move to Azure AD P2 Conditional Access and have users who are on P1 MFA, then in order to move them over, you have to disable and re-enable MFA on their account - or at least that's what one PFE told me. The problem is, when you do that, you lose their options like if they prefer to enter a code from the app, receive a text, etc. by default. Wouldn't it be nice if you could keep that stuff?

Well, you can!

<!--more-->

Here's a PowerShell function I wrote that performs this task. It assumes you've already done a <strong>Connect-MsolService</strong> and logged in successfully.
<pre class="lang:default decode:true ">function Move-MfaSettings {
    &lt;#
    .SYNOPSIS
        Converts a user from classic MFA to modern MFA and retains their settings.
    .DESCRIPTION
        Takes a MSOL user and manipulates their settings to engage modern MFA without overwriting their current preferences.
    .EXAMPLE
        PS&gt; Move-MfaSettings -User $(Get-MsolUser -UserPrincipalName myguy@domain.tld) 
        If a user with the UPN myguy@domain.tld is found, the MFA settings will be updated.
    #&gt;
    [cmdletbinding(SupportsShouldProcess)]
    param (
        [parameter(Mandatory, ValueFromPipeline)]
        #The MSOL user object whose MFA settings are being adjusted
        [Microsoft.Online.Administration.User]$User
    )
    if ($PSCmdlet.ShouldProcess("Converting user $($User.UserPrincipalName) from classic MFA to modern MFA")) {
        $strongAuthMethods = $User.StrongAuthenticationMethods | Select-Object MethodType, IsDefault
        $setStrongAuthMethods = @()
        foreach ($strongAuthMethod in $strongAuthMethods) {
            $add = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationMethod
            $add.IsDefault = $strongAuthMethod.IsDefault
            $add.MethodType = $strongAuthMethod.MethodType
            $setStrongAuthMethods += $add
        }
        $null = Set-MsolUser -UserPrincipalName $User.UserPrincipalName -StrongAuthenticationRequirements @() -StrongAuthenticationMethods $setStrongAuthMethods
    }
}</pre>
It could probably stand for a better name, but I've called it <strong>Move-MfaSettings</strong>, and it takes one parameter: a MSOL user object. It supports the -WhatIf flag, by implementing SupportsShouldProcess.

On line 18, I'm storing the Strong Authentication Methods of the user object that was passed to the function. All I need out of here is the MethodType and IsDefault properties. This is the option/preference information that we would normally lose by performing this task. We're going to lose it again, but since we've saved it here, we can rebuild and add it back later.

Lines 20 through 25 go through each of the preferences we collected on Line 18 and builds a new StrongAuthenticationMethod object out of them. Then we set the IsDefault and MethodType property for each one, and store the new object in an array.

Finally, on line 26, I've used <strong>Set-MsolUser</strong> to disable the Strong Authentication Requirements, and set the Strong Authentication Methods to the array of those objects we created.

Now you can disable MFA for users while still keeping their settings, which is pretty handy when you're transitioning to P2 Conditional Access.
