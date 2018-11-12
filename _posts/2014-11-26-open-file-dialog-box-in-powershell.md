---
layout: post
title: Open File Dialog Box In PowerShell
date: 2014-11-26 16:30
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, PowerShell ISE]
---
Here's a neat little PowerShell function you can throw into your scripts. Lots of times I want to specify a CSV or TXT or some other file in a script. It's easy to do this:
```
$inputfile = read-host "Enter the path of the file"
$inputdata = get-content $inputfile\n```
But that means you have to type the whole absolute or relative path to the file. What a pain. I know what you're thinking... <strong>There must be a better way!</strong>

There is! Use an open file dialog box. You know, like when you click File, Open and a window opens and you navigate your filesystem and select a file using a GUI. How do you do it in PowerShell? Let me show you. First things first: let's declare a function with a couple of the items we're going to need.
```
Function Get-FileName($initialDirectory)
{
    [System.Reflection.Assembly]::LoadWithPartialName("System.windows.forms") | Out-Null
}\n```
I'm going to name this function Get-FileName because I like the Verb-Noun naming scheme that PowerShell follows. It's got a parameter, too. $initialDirectory is the directory that our dialog box is going to display when we first launch it. The part of this that most likely looks new is line 3. We need to load a .NET item so we can use the Windows Forms controls. We're loading via partial name because we want all the Windows Form controls, not just some. It's faster and easier to do this than it is to pick and choose. We're piping the output to Out-Null because we don't want all the verbose feedback it gives when it works.

Now let's open the thing and get to business selecting a file.
```
Function Get-FileName($initialDirectory)
{
    [System.Reflection.Assembly]::LoadWithPartialName("System.windows.forms") | Out-Null
    
    $OpenFileDialog = New-Object System.Windows.Forms.OpenFileDialog
    $OpenFileDialog.initialDirectory = $initialDirectory
    $OpenFileDialog.filter = "CSV (*.csv)| *.csv"
    $OpenFileDialog.ShowDialog() | Out-Null
}\n```
On line 5, we're creating a new object. That object is unsurprisingly an OpenFileDialog object. On line 6 we're specifying that initial directory that we got in the parameter. On line 7 we're doing something a little interesting. The filter attribute of the OpenFileDialog object controls which files we see as we're browsing. That's this part of the box.

<img class="alignnone wp-image-628 size-full" src="/wp-content/uploads/2014/11/OpenFileDialog.png" alt="" width="818" height="71" />

I'm limiting my files to CSV only. The first part of the value is CSV (<em>.csv) which is what the dialog box shows in the menu. The second part after the pipe character *.csv is the actual filter. You could make any kind of filter you want. For instance, if you wanted to only see files that started with "SecretTomFile", you could have a filter like SecretTomFile</em>.

The next item on line 8 is to open the dialog box, we do that with the ShowDialog() function. We discard the output from this command because it's spammy in this context, just like when we added the .NET items.

One last thing! We've created, defined and opened our OpenFileDialog box but don't we actually need to get the result of what file was selected? Yes, we do. That's pretty easy, though.
```
Function Get-FileName($initialDirectory)
{
    [System.Reflection.Assembly]::LoadWithPartialName("System.windows.forms") | Out-Null
    
    $OpenFileDialog = New-Object System.Windows.Forms.OpenFileDialog
    $OpenFileDialog.initialDirectory = $initialDirectory
    $OpenFileDialog.filter = "CSV (*.csv)| *.csv"
    $OpenFileDialog.ShowDialog() | Out-Null
    $OpenFileDialog.filename
}\n```
The Filename attribute is set when someone commits to opening a file in the OpenFileDialog box. On line 9, we're returning it to whatever called our script.

So to use this function in the same way as the example at the top of this post, your code would look like this.
```
$inputfile = Get-FileName "C:\temp"
$inputdata = get-content $inputfile\n```
I think this is a lot nicer than typing a filename every time you want to run a script. I find it particularly convenient on scripts I run a lot.
