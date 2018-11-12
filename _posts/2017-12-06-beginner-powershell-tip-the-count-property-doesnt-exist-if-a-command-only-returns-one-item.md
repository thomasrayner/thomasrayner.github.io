---
layout: post
title: Beginner PowerShell Tip - The .Count Property Doesn't Exist If A Command Only Returns One Item
date: 2017-12-06 07:00
author: thmsrynr
comments: true
categories: [active directory, active directory, array, beginner series, beginner series, collections, PowerShell, powershell, Uncategorized]
---
If you’re just getting started in PowerShell, it’s possible that you haven’t bumped into this specific issue yet. Perhaps you've got a variable <em>$users</em> and you're assigning it a value like this.
<pre class="lang:ps decode:true">PS&gt; $users = Get-ADUser -Filter "samaccountname -like '*thmsrynr'"</pre>
This will get all the users in your Active Directory whose username ends with "thmsrynr".

Great! Now how many users got returned? We can check the Count property to find out.

<!--more-->
<pre class="lang:ps decode:true">PS&gt; $users.Count
3</pre>
Looks like there are three users in my AD that got returned. Now the problem at hand, what if there's only one user returned? What if only one user in my AD has that kind of username? I'll end up with this.
<pre class="lang:ps decode:true">PS&gt; $users.Count
# Nothing gets returned...</pre>
Even though I can do this and see there is one user in there.
<pre class="lang:ps decode:true">PS&gt; $users

DistinguishedName : CN=ThmsRynr,OU=Users,DC=PCLINC,DC=domain,DC=tld
Enabled           : True
GivenName         : Thomas
Name              : Thomas Rayner
ObjectClass       : user
ObjectGUID        : &lt;snip&gt;
SamAccountName    : ThmsRynr
SID               : &lt;snip&gt;
Surname           : Rayner
UserPrincipalName : thmsrynr@outlook.com</pre>
What if I was doing something like this?
<pre class="lang:ps decode:true ">if ($users.Count -gt 0) {
    # Do something
}
else {
    # Do something else
}</pre>
Since <em>$users.Count</em> is null even when there's one user in there, my if statement won't work correctly. Well, you can take a bit of a shortcut and do something a bit different when you're assigning a value to <em>$users</em>.
<pre class="lang:ps decode:true ">$users = @(Get-AdUser -Filter "samaccountname -like '*thmsrynr'")</pre>
By wrapping the command in <strong>@( )</strong> we are forcing <em>$users</em> to be an array even if only one item is returned.

This issue happens because PowerShell loves to unroll arrays and other collections for you. By doing this workaround, if there's only one AD user whose username ends in thmsrynr, you'll still end up with an array with a single item in it, and <em>$users.Count</em> will return "1" like you expected.
