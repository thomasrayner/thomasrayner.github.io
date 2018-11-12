---
layout: post
title: PowerShell 10 Year Anniversary Code Golf Winners
date: 2016-11-21 10:32
author: thmsrynr@outlook.com
comments: true
categories: [code golf, codegolf, mvp, nshr, Pester, pester, PowerShell, powershell, powershell10year]
---
For the PowerShell 10 Year Anniversary, Will Anderson (<a href="http://twitter.com/gamerlivingwill" target="_blank">@GamerLivingWill</a> on Twitter) and I (<a href="http://twitter.com/mrthomasrayner" target="_blank">@MrThomasRayner </a>on Twitter) ran a three-hole code golf competition on <a href="http://www.code-golf.com" target="_blank">code-golf.com</a>, a site developed by fellow MVP Adam Driscoll.

Here is the link to all the background info on the competition: <a href="https://github.com/ThmsRynr/PS10YearCodeGolf" target="_blank">https://github.com/ThmsRynr/PS10YearCodeGolf</a> . Check this page out for links to the individual holes, too.

So, without further delay, let's announce the winners!

<h3>Hole 1</h3>

The challenge was to get all the security updates installed on the local computer in the last 30 days and return the results in the form of a [Microsoft.Management.Infrastructure.CimInstance] object (or an array of them).

The winner of this hole is <a href="https://github.com/SimonWahlin" target="_blank">Simon Wåhlin</a>. Here is their 46 character submission.

```
gcim(gcls *ix*|% *mC*e)|? I*n -gt((date)+-30d)
```

<strong>gcls &#42;ix&#42; </strong>gets the CimClass <em>win32_quickfixengineering</em> and <strong>% &#42;mC&#42;e </strong>gets the <em>CimClassName</em> property. <strong>gcim</strong> is an alias for <strong>Get-CimInstance </strong>which, as per the previous section, is getting the <em>win32_quickfixengineering</em> class. The results are piped into the <strong>where-object</strong> cmdlet where the property matching the pattern <strong>I*n</strong> (which happens to be <em>InstalledOn</em>) is greater than the current date, minus 30 days.

<h3>Hole 2</h3>

The challenge was to get the top ten file extensions in c:\windows\system32, only return 10 items and group results by extension.

The winner of this hole is <a href="https://github.com/SimonWahlin" target="_blank">Simon Wåhlin</a> again. Here is their 42 character submission.

```
(ls C:\*\s*2\*.*|% E*n|group|sort c* -d)[0..9]
```

<strong>ls c:&#92;&#42;&#92;s&#42;2&#92;&#42;.&#42;</strong> means <strong>Get-ChildItem</strong> where the path is c:\<em>&lt;any directory&gt;\&lt;a directory matching s&#42;2&gt;\&lt;files, not directories&gt; </em>and this pattern only matches the path c:\windows\system32\&lt;files&gt;. This is piped into the <strong>foreach-object</strong> cmdlet to retrieve the property that matches the pattern <strong>E&#42;n</strong>,<strong> </strong>which is the <em>Extension</em> property. The extensions are piped into the <strong>sort-object</strong> cmdlet, sorted by the property that matches the pattern <strong>c&#42;,</strong> which is count, and returned in descending order. This is an array, and the items in positions 0-9 are returned.

There were shorter submissions for this hole that didn't explicitly target c:\windows\system32 and therefore missed the challenge. You could not assume we were already on c: or running as admin, etc. Some solutions included folders in the results which also missed the challenge.

<h3>Hole 3</h3>

The challenge was to get all the active aliases that are fewer than three characters long and do not resolve to a Get- command. For this hole, even though it wasn't in the Pester test, you had to assume that non-standard aliases might be on the system. That's why we specifically mentioned that we didn't want you to return aliases that resolve to Get-&#42;, and the Pester test checked the <em>ResolvedCommand.Name</em> property of the aliases you returned.

To break some submissions that didn't check what the aliases resolved to, you could just run <strong>New-Alias x Get-ChildItem</strong> to create a new alias of 'x' that resolves to Get-ChildItem.

The winner of this hole is <a href="https://github.com/EdijsPerkums" target="_blank">EdijsPerkums</a>. Here is their 24 character submission.

```
gal ?,??|? Di* -Notm Get
```

<strong>Get-Alias </strong>is passed an array of regex patterns, <strong>?,??</strong> which corresponds to one and two characters. The results are piped into the <strong>where-object</strong> cmdlet to isolate aliases whose property that matches the pattern <strong>Di&#42;</strong> (DisplayName) doesn't match <strong>Get</strong>.

Congratulations to all the winners! We will be in touch to get you your prizes. We hope you all had fun with this mini-competition. Don't forget to check out all the terrific material from the<a href="https://channel9.msdn.com/Events/PowerShell-Team/PowerShell-10-Year-Anniversary" target="_blank"> PowerShell 10 Year Anniversary on Channel 9</a>!
