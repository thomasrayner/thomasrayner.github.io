---
layout: post
title: Quick Tip - Use PowerShell To Detect If A Location Is A Directory Or A Symlink
date: 2015-03-18 08:30
author: thmsrynr@outlook.com
comments: true
categories: [get-item, PowerShell, powershell, PowerShell ISE, powershell ise, quick tip, symbolic link, symlink]
---
In PowerShell, <a title="Wikipedia - NTFS Symbolic Links" href="http://en.wikipedia.org/wiki/NTFS_symbolic_link" target="_blank">symbolic links (symlinks)</a> appear pretty transparently when you're simply navigating the file system. If you're doing other work, though, like changing ACLs, bumping into symlinks can be a pain. Here's how to tell if a directory in question is a symlink or not.

Consider the following commands.

<pre class="lang:ps decode:true ">PS C:\Users\ThmsRynr&gt; ((get-item c:\symlink).Attributes.ToString())
Directory, ReparsePoint

PS C:\Users\ThmsRynr&gt; ((get-item c:\normaldir).Attributes.ToString())
Directory</pre>

Here, we're just running a <strong>Get-Item</strong> command on two locations, getting the Attributes property and converting to a string. The first item is a symlink and includes "ReparsePoint" in its attributes. The second item is a normal directory and does not include "ReparsePoint".

So that means we can do something as easy as this.

<pre class="lang:ps decode:true ">PS C:\Users\ThmsRynr&gt; ((get-item c:\symlink).Attributes.ToString() -match "ReparsePoint")
True

PS C:\Users\ThmsRynr&gt; ((get-item c:\normaldir).Attributes.ToString() -match "ReparsePoint")
False</pre>

Easy. If the above values have "ReparsePoint" in them, we know they are a symlink and not just a regular directory. In my case, my script to apply ACLs to a group of directories avoided symlinks with ease.
