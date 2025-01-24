---
layout: post
title: Messing Around With PowerShell 6
date: 2018-11-21
author: thmsrynr
comments: true
categories: [all for fun, C#, C#, New Stuff, open source, oss, PowerShell, powershell]
---
Starting with PowerShell 6, the whole language is open source. You've probably heard about that already. But if you don't think of yourself as a "developer", then it's possible that the most you've ever taken advantage of that fact is creating a GitHub issue or commenting on a PR. Today, follow along with me, and we'll change that.

If you're at all comfortable writing PowerShell, you'll be able to pick up C# with relative convenience. To be fair, dabbling with editing PowerShell is pretty far removed from a "Hello world" exercise, but maybe it'll be fun enough to motivate you to learn more. The deeper you get into PowerShell, the more learning some C# might help you.

So, let's get at it. First, clone the repository with `git clone https://github.com/powershell/powershell.git` or fork it and clone your fork. Check out the [contribution guide](https://github.com/powershell/powershell#building-the-repository) for information on how to prep your environment and build your own `pwsh.exe` from the source.

Then, open the `PowerShell.sln` file in Visual Studio, or open up the project in VS Code. I tend to prefer "full blown" Visual Studio for writing C#, because it's what I'm used to, but VS Code is perfectly fine, with a couple extensions added on (which are recommended as soon as you start looking at C# stuff).

So, now, what do you want to do? I like to start simple. When you first launch `pwsh.exe` there's a banner message that is displayed, which at the time of this writing reads something like:

```
PowerShell 6.1.0
Copyright (c) Microsoft Corporation. All rights reserved.

https://aka.ms/pscore6-docs
Type 'help' to get help.
```

Let's make that more interesting. Probably, there's a string somewhere that we can just edit and make it say whatever we want.

If you expand `powershell-win-core`, you'll see `Program.cs` which is probably what gets run when you fire up `pwsh.exe` in Windows. At least, when I started poking around, that was my guess. It seems pretty simple. It returns an `UnmanagedPSEntry`.

Look at the definition of the `UnmanagedPSEntry` class (by right clicking on it and selecting "Go to definition"), and you can read the code for the `Start()` method that is called in `Program.cs`. Eventually, you'll get to around line 70 in the file that defines `UnmanagedPSEntry` (at the time of this writing) where a variable named `banner`, and another one named `formattedBanner` are assigned a value. The `banner` value seems to come from another class called `ManagedEntranceStrings` so maybe let's take a look at that. That name alone sort of sounds like the type of thing we want to mess with right now.

The `ManagedEntranceStrings` class which, as the comment in the file suggests, returns the cached ResourceManager instance used by the class. It looks like it's located at `"Microsoft.PowerShell.ConsoleHost.resources.ManagedEntranceStrings"`. So... let's go peek in there. It's a resx file.

Aha! Looks like maybe we found it. There's a `ShellBannerNonWindowsPowerShell` item that looks like we can fudge around with. I'm just going to make it a little more casual.

Save everything, follow the above linked directions to build PowerShell, and launch the `pwsh.exe` that it created. You should see your new message. Mine looks like this.

```
Welcome to PowerShell 6.1.0. If you're stuck, type 'help', otherwise, check out the docs.
```

It's the little things that add the most joy to life. In all honesty though, explore a bit and you'll start to learn about how PowerShell **really** works, and next time you see something that doesn't work like you think it should, you'll have more power to do something about it.