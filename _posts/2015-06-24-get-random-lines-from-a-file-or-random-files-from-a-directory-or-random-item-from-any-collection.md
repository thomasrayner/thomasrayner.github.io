---
layout: post
title: Get Random Lines From A File (Or Random Files From A Directory... Or Random Item From Any Collection)
date: 2015-06-24 08:30
author: thmsrynr@outlook.com
comments: true
categories: [get-random, PowerShell, powershell, PowerShell ISE, powershell ise]
---
Don't ask me why but I recently had a need to get a random line from a text file. There's a small piece of strange behavior that I came across with the cmdlet I chose to use: <strong>Get-Random</strong><strong>. </strong><strong>Get-Random</strong> does what it sounds like. It's commonly used for getting random numbers (see <a href="http://www.workingsysadmin.com/quick-tip-get-random-is-weird-doesnt-include-the-maximum-value/" target="_blank">this post I wrote a while ago</a> about a gotcha with this behavior) but you can also pass it an input object.

For this example, I have a file in my c:\temp folder named random.txt. It's contents just look like this.

<pre class="lang:ps decode:true">so
many
random
words
to
choose
from
which
one
will
be
picked?</pre>

So since <strong>Get-Random</strong> includes an -InputObject parameter, I should just be able to do the following, right?

<pre class="lang:ps decode:true ">Get-Random -InputObject C:\temp\random.txt</pre>

Well, if you were hoping it would be that easy, I'm afraid I've got some bad news. Every time you run this command, the InputObject specified is always the value returned.

<img class="alignnone size-full wp-image-199" src="http://www.workingsysadmin.com/wp-content/uploads/2015/04/getrandom1.png" alt="getrandom1" width="636" height="180" />

Well that's not very helpful for a guy looking for a random line from the file. Turns out that -InputObject is looking for a collection of items, it's not doing the work of examining the path to the file and extracting the data from it. That's easy enough to get around. We'll just do that work ourselves.

<pre class="lang:ps decode:true ">Get-Random -InputObject (get-content C:\temp\random.txt)</pre>

There we go. Get a random item from the collection returned by <strong>Get-Content <span style="text-decoration: underline;">C:\Temp\Random.txt</span></strong>. Then you get output like this.

<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/04/getrandom2.png"><img class="alignnone size-full wp-image-200" src="http://www.workingsysadmin.com/wp-content/uploads/2015/04/getrandom2.png" alt="getrandom2" width="768" height="329" /></a>

You could get a random file from a directory like this.

<pre class="lang:ps decode:true ">Get-Random -InputObject (get-childitem c:\temp\)</pre>

Or, indeed, pass any array or hash table. Here's an example of getting a random property from the $Host variable.

<pre class="lang:ps decode:true ">$Host | Select-Object (Get-Random -InputObject ($Host | Get-Member -MemberType Property).Name)</pre>

<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/04/getrandom3.png"><img class="alignnone size-large wp-image-201" src="http://www.workingsysadmin.com/wp-content/uploads/2015/04/getrandom3-1024x315.png" alt="getrandom3" width="604" height="186" /></a>

&nbsp;

&nbsp;

&nbsp;
