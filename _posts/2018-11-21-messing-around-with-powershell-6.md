---
layout: post
title: Messing Around With PowerShell 6
date: 2018-11-21 07:30
author: thmsrynr
comments: true
categories: [all for fun, C#, C#, New Stuff, open source, oss, PowerShell, powershell]
published: false
---
Starting with PowerShell 6, the whole thing is open source. You've probably heard that already. But if you don't think of yourself as a "developer", then it's possible that the furthest you've ever taken advantage of that fact is creating a GitHub issue or commenting on a PR. Today, follow along with me, and we'll change that.

<!--more-->

If you're at all comfortable writing PowerShell, you'll be able to pick up C# with relative convenience. To be fair, dabbling with editing PowerShell is pretty far removed from a "Hello world" exercise, but maybe it'll be fun enough to motivate you to learn more. The deeper you get into PowerShell, the more learning some C# might help you.

So, let's get at it. First, clone the repository with <code>git clone https://github.com/powershell/powershell.git</code> or fork it and clone your fork. Check out the contribution guide <a href="https://github.com/powershell/powershell#building-the-repository" target="_blank" rel="noopener">for information</a> on how to prep your environment and build your own <code>pwsh.exe</code> from the source.

Then, open the PowerShell.sln file in Visual Studio, or open up the project in VS Code. I tend to prefer "full blown" Visual Studio for writing C#, because it's what I'm used to, but VS Code is perfectly fine, with a couple extensions added on (which are recommended as soon as you start looking at C# stuff).

So, now, what do you want to do? I like to start simple. When you first launch <code>pwsh.exe</code> there's a banner message that is displayed, which at the time of this writing reads something like:
<pre>PowerShell {0}
Copyright (c) Microsoft Corporation. All rights reserved.

https://aka.ms/pscore6-docs
Type 'help' to get help.
```
So, let's make that more interesting. Probably there's a string somewhere that we can just edit and make it say whatever we want.

If you expand <code>powershell-win-core</code> , you'll see <code>Program.cs</code> which is probably what gets run when you fire up <code>pwsh.exe</code> in Windows. At least, when I started poking around, that was my guess. It seems pretty simple. It returns an <code>UnmanagedPSEntry</code>.

Look at the definition of the <code>UnmanagedPSEntry</code> class, and you can read the code for the <code>Start()</code> method that is called in <code>Program.cs</code>. Eventually, you'll get to around line 70 (at the time of this writing) where a variable named banner, and another one named formattedBanner are assigned a value. The banner value seems to come from another class called <code>ManagedEntranceStrings</code> so maybe let's take a look at that.

The <code>ManagedEntranceStrings</code> class, as the comment in the file suggests, returns the cached ResourceManager instance used by the class. It looks like it's located at <code>"Microsoft.PowerShell.ConsoleHost.resources.ManagedEntranceStrings"</code>. So... let's go peek in there. It's a resx file.

Aha! Looks like maybe we found it. There's a <code>ShellBannerNonWindowsPowerShell</code> item that looks like we can fudge around with. I'm just going to add a message of my own in addition to what's already there.

Save everything, follow the above linked directions to build PowerShell, and launch the <code>pwsh.exe</code> that it created. You should see your new message. Mine looks like this.
<div>
<pre>PowerShell {0}
Copyright (c) Microsoft Corporation. All rights reserved.

https://aka.ms/pscore6-docs
Type 'help' to get help. Or otherwise just do your thing, man.
```
</div>
<div></div>
<div>It's the little things that add the most joy to life. In all honesty though, explore a bit and you'll start to learn about how PowerShell <em>really</em> works, and next time you see something that doesn't work like you think it should, you'll have more power to do something about it.</div>
