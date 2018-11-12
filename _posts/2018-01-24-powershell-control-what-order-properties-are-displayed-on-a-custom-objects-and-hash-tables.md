---
layout: post
title: PowerShell - Control What Order Properties Are Displayed On A Custom Objects And Hash Tables
date: 2018-01-24 07:30
author: thmsrynr
comments: true
categories: [hash table, hashtable, ordered objects, PowerShell, powershell]
---
There are a handful of different ways to create custom objects in PowerShell, including building one from a hash table. You might do something like this.
```
PS&gt; $props = @{'prop1' = 1; 'prop2' = 2}
PS&gt; $obj = New-Object -TypeName PSObject -Property $props\n```
But then, just run <strong>$obj</strong> and see what you get. This is what I got.
```
PS&gt; $obj

prop2 prop1
----- -----
    2     1\n```
It put prop2 before prop1 even though I put prop1 first in the hash table! Most of the time, this doesn't matter, but what about when it does?

<!--more-->

Sure, you could use <strong>Select-Object</strong> to accomplish this.
```
PS&gt; $obj | Select-Object -Property prop1,prop2

prop1 prop2
----- -----
    1     2\n```
But that seems excessively verbose and inefficient. Luckily there is a better way. Introducing Ordered Hash Tables!

Ordered hash tables are pretty much what they sound like. By default, a hash table is a collection of objects (key and value pairs) whose order isn't important. An ordered hash table is the same thing, but where the order they are in the hash table matters, and they're pretty easy to use. Our first lines of code from this example becomes this.
```
PS&gt; $props = [ordered]@{'prop1' = 1; 'prop2' = 2}
PS&gt; $obj = New-Object -TypeName PSObject -Property $props\n```
Just add the <em>[ordered]</em>  accelerator to the hash table, and now PowerShell will respect the order that you enter items into your hash table.

&nbsp;
