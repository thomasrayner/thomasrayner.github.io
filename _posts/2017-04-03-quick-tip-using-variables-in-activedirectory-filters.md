---
layout: post
title: Quick Tip - Using Variables In ActiveDirectory Filters
date: 2017-04-03 08:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, activedirectory, Automation, filters, PowerShell, powershell, variables]
---
If you work with the ActiveDirectory PowerShell module, you've probably used the <em>-filter</em> parameter to search for accounts or objects in Active Directory. You've probably wanted to use variables in those filters, too.

Say you have a command from something like an remote Exchange management shell, that returned an object that includes a username (called Alias in this example).

```
$person = (Get-Mailbox ThmsRynr).Alias
```

And let's use that in an ActiveDirectory command. Ignoring the fact that you could find the account that has this username without using a filter, let's see how you would use it in a filter.

You might try this.

```
Get-AdUser -Filter "SamAccountName -eq $person"
```

But you'd get errors.

```
Get-AdUser : Error parsing query: 'SamAccountName -eq ThmsRynr' Error Message: 'syntax error' at position: '20'.
At line:1 char:1
+ Get-AdUser -Filter "SamAccountName -eq $person"
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ParserError: (:) [Get-ADUser], ADFilterParsingException
    + FullyQualifiedErrorId : ActiveDirectoryCmdlet:Microsoft.ActiveDirectory.Management.ADFilterParsingException,Microsoft.ActiveDirectory.Management.Commands.GetADUser
```

That's because the filter can't handle your variable that way. To use a variable in an ActiveDirectory cmdlet filter, you need to wrap the filter in curly braces.

```
Get-AdUser -Filter {SamAccountName -eq $person}
```

And you get your results!

```
DistinguishedName : CN=Thomas Rayner,OU=Users,DC=lab,DC=workingsysadmin,DC=com
Enabled           : True
GivenName         : Thomas
Name              : Thomas Rayner
ObjectClass       : user
ObjectGUID        : &lt;snip&gt;
SamAccountName    : TFRayner
SID               : &lt;snip&gt;
Surname           : Rayner
UserPrincipalName : ThmsRynr@outlook.com
```

Pretty easy fix for a pretty silly issue.
