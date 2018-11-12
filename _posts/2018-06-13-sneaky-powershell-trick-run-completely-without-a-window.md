---
layout: post
title: Sneaky PowerShell Trick: Run Completely Without A Window
date: 2018-06-13 07:30
author: thmsrynr
comments: true
categories: [C#, C#, PowerShell, powershell, sneaky]
---
Maybe you have a login script or something else that's written in PowerShell that you want to run without having any kind of window pop up - not even a blank one. There's a few ways to do this, but my current favorite is to wrap it in C#. Thanks <a href="https://twitter.com/markekraus" target="_blank" rel="noopener">Mark Kraus</a> for this tip!

<!--more-->

Fire up Visual Studio, and create a new C# console application. Right click and change the properties of the project so that the output type is Window App... and then get this... <em>don't make a window</em>.

From there, you'll need to add a reference for <strong>PowerShellStandard.Library</strong> so you can do PowerShell-y business in your C# application. After that, you can make a method look like this.
<pre class="lang:c# decode:true ">static void Main(string[] args)
{
    var powershell = PowerShell.Create();
    powershell.AddScript(@"
Get-ChildItem -Path c:\temp | out-file c:\temp\shh.txt
");
    var handler = powershell.BeginInvoke();
    while (!handler.IsCompleted)
        Thread.Sleep(200);
    powershell.EndInvoke(handler);
    powershell.Dispose();
}</pre>
It's not super complicated code. Line 3 creates a new PowerShell object so we can, you know, run PowerShell code. On Line 4 - 6, we're adding the script that's going to be executed. You could retrieve the code from a file, but I've just stuck a here-string in there. My script is pretty simple, it's just getting all the items in my c:\temp folder and exporting that output to a file named shh.txt.

After that, I've got to actually run my code. That happens on Line 7, and then on Line 8 and 9, we make the thread wait until the code is done executing. Then finally on Line 10 and 11, I'm cleaning up after myself by ending the invocation and disposing of my PowerShell object.

You can build this, and then look in the folder for your app, in the bin\Debug folder, you'll find an .exe file which you can run. Double click it and you shouldn't see any window pop up, no console, no XAML window, no nothing, but your PowerShell script will run. If you made yours look like mine, go check for that file that it should have created.

Now when your login script runs, your users won't be able to close it before it finishes!
