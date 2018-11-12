---
layout: post
title: New Stuff: Get-Clipboard And Set-Clipboard - New In PowerShell 5.0
date: 2015-05-13 08:30
author: thmsrynr@outlook.com
comments: true
categories: [filesystem, get-clipboard, New Stuff, new stuff, PowerShell, powershell, PowerShell 5.0, powershell 5.0, PowerShell ISE, powershell ise, set-clipboard]
---
Predictably, there are lots of new cmdlets coming in PowerShell/Windows Management Framework 5.0. Two of them that just came out in build 10105 are the <strong>Get-Clipboard</strong> and <strong>Set-Clipboard</strong> cmdlets. The help docs aren't all written at the time I'm writing this post but I wanted to introduce them and highlight a couple neat use cases I immediately thought of.

[caption id="attachment_211" align="alignnone" width="1122"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/05/5-1-2015-7-49-29-AM.png" target="_blank"><img class="size-full wp-image-211" src="http://www.workingsysadmin.com/wp-content/uploads/2015/05/5-1-2015-7-49-29-AM.png" alt="New Get-Clipboard and Set-Clipboard cmdlets" width="1122" height="718" /></a> New Get-Clipboard and Set-Clipboard cmdlets (click for larger)[/caption]

Back in the old days of PowerShell 4.0, you had to pipe output to clip.exe or use the <a href="https://pscx.codeplex.com/" target="_blank">PowerShell Community Extensions</a> to interact with your clipboard. Not anymore!

Looking at the <strong>Get-Clipboard</strong> syntax, it's quickly apparent that you can do more than just get the clipboard's text content but let's start with that anyway. So, what if I go and select some text, right click and copy it. What can I do with the <strong>Get-Clipboard</strong> cmdlet?

<pre class="lang:ps decode:true ">PS C:\&gt; Get-Clipboard
I copied this text to my clipboard.</pre>

Not exactly mind blowing. Similarly, you can use the <strong>Set-Clipboard</strong> cmdlet to put text on the clipboard.

<pre class="lang:ps decode:true ">PS C:\&gt; "This text was put on the clipboard using new cmdlets." | Set-Clipboard

PS C:\&gt; Get-Clipboard
This text was put on the clipboard using new cmdlets.</pre>

I'm probably not blowing your mind with this one either. Where this gets fun is when you consider the possibilities the using the <em>-Format</em> parameter. I can put more than just text on my clipboard, right? Let's see what I get when I copy three files in my c:\temp directory to my clipboard. If I try to just use <strong>Get-Clipboard</strong> without any additional parameters or info like I did in the above examples, I won't get anything returned, but what I can do is this.

<pre class="lang:ps decode:true ">PS C:\&gt; Get-Clipboard -Format FileDropList


    Directory: C:\temp


Mode                LastWriteTime         Length Name                                                                                                                 
----                -------------         ------ ----                                                                                                                 
-a----         5/1/2015   8:02 AM             30 file1.txt                                                                                                            
-a----         5/1/2015   8:02 AM             18 file2.txt                                                                                                            
-a----         5/1/2015   8:02 AM             11 file3.txt</pre>

Now we're doing cool things. And what kind of objects are these?

<pre class="lang:ps decode:true ">PS C:\&gt; (Get-Clipboard -Format FileDropList)[0].GetType()

IsPublic IsSerial Name                                     BaseType                                                                                                   
-------- -------- ----                                     --------                                                                                                   
True     True     FileInfo                                 System.IO.FileSystemInfo</pre>

FileInfo! We can do all the same things with this array of files that we would do to the results of a <strong>Get-ChildItem</strong> command. This means we can go the other way too and use the <strong>Set-Clipboard</strong> cmdlet to put a bunch of files onto the clipboard.

<pre class="lang:ps decode:true ">PS C:\&gt; Get-ChildItem c:\temp\file*.txt  | Set-Clipboard

PS C:\&gt; Get-Clipboard -Format FileDropList


    Directory: C:\temp


Mode                LastWriteTime         Length Name                                                                                                                 
----                -------------         ------ ----                                                                                                                 
-a----         5/1/2015   8:02 AM             30 file1.txt                                                                                                            
-a----         5/1/2015   8:02 AM             18 file2.txt                                                                                                            
-a----         5/1/2015   8:02 AM             11 file3.txt</pre>

Note with all of the above examples, you can use the <em>-Append</em> parameter to simply add on to whatever is already on the clipboard.

I won't cover the other formats (Image and Audio) or the text format types because you need something to discover for yourself. The last thing I'll point out is that you can easily clear the clipboard, too.

<pre class="lang:ps decode:true ">PS C:\&gt; $null | Set-Clipboard

PS C:\&gt; Get-Clipboard

PS C:\&gt;</pre>

I'm not going to cover every new cmdlet that comes out with PowerShell 5.0 but this one is very accessible and I think I'll be able to use it all over the place.
