---
layout: post
title: The Difference Between Get-Member and .GetType() in PowerShell
date: 2017-09-27 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, get-member, gettype, PowerShell, powershell, working with objects]
---
Recently, I was helping someone in a forum who was trying to figure out what kind of object their command was returning. They knew about the standard cmdlets people suggest when you're getting started (<strong>Get-Help</strong>, <strong>Get-Member</strong>, and <strong>Get-Command</strong>), but couldn't figure out what was coming back from a specific command.

<!--more-->

In order to make this a more generic example, and to simplify it, let's approach this differently. Say I have these two objects where one is a string and the other is an array of two strings.

<pre class="lang:ps decode:true">PS&gt; $thing1 = 'This is an item'
PS&gt; $thing2 = @('This is another item','This is one more item')
PS&gt; $thing1; $thing2</pre>

The third line shows you what you get if you write these out to the screen.

<pre class="lang:ps decode:true ">This is an item
This is another item
This is one more item</pre>

It looks like three separate strings, right? Well we should be able to dissect these with <strong>Get-Member</strong> to get to the bottom of this and identify the types of objects these are. After all, one is a string and the other is an array, right?

<pre class="lang:ps decode:true">PS&gt; $thing1 | Get-Member


   TypeName: System.String

Name             MemberType            Definition
----             ----------            ----------
Clone            Method                System.Object Clone()
&lt;output truncated&gt;</pre>

So far, so good. $thing1 is our string, so we'd expect the TypeName to be System.String. Let's check the array.

<pre class="lang:ps decode:true ">PS&gt; $thing2 | Get-Member


   TypeName: System.String

Name             MemberType            Definition
----             ----------            ----------
Clone            Method                System.Object Clone()
&lt;output truncated&gt;</pre>

Dang, $thing2 is an array but <strong>Get-Member</strong> is still saying the TypeName is System.String. What's going on?

Well, the key here is what we're doing is writing the output of $thing2 into <strong>Get-Member</strong>. So the output of $thing2 is two strings, and that's what's actually hitting <strong>Get-Member</strong>. If we want to see what kind of object $thing2 really is, we need to use a method that's built into every PowerShell object: GetType().

<pre class="lang:ps decode:true ">PS&gt; $thing2.GetType()

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     True     Object[]                                 System.Array</pre>

There you go. $thing2 is a System.Array object, just like we thought.

<strong>Get-Member</strong> is useful for exploring objects properties and methods, as well as their type. In this case, however, it was exploring the object that was being passed to it through the pipeline.
