---
layout: post
title: Quick Script Share - Get-RandomPW - Create Random Passwords
date: 2015-12-02 08:30
author: thmsrynr@outlook.com
comments: true
categories: [get-random, password, PowerShell, powershell, PowerShell ISE, powershell ise, script share]
---
I had a need to repeatedly create random passwords of varying lengths. To satisfy this need, I wrote the following basic script.

<pre class="lang:ps decode:true">function Get-RandomPW
{
    param
    (
        [int]$Length = 16
    )
    $arrChars = 'abcdefghkmnprstuvwxyzABCDEFGHKLMNPRSTUVWXYZ123456789!@#$%^&amp;*()-=_+'.ToCharArray()
    $sRandomString = -join $(1..$Length | Foreach-Object { Get-Random -InputObject $arrChars })
    return $sRandomString
}</pre>

On line 1, you can see I named my function <strong>Get-RandomPW </strong>which I did because I like following the standard Verb-Noun naming scheme that PowerShell functions and cmdlets are supposed to follow. On lines 3 through 6, I'm declaring my only parameter, $Length. $Length is an integer which will represent the length of the password we want. By default, I create a 16 character password.

On line 7, $arrChars is declared and assigned the value of all the valid characters for my password. I list all the characters in one big string and convert to a Char array because it's easier to look at and manage, in my opinion.

On line 8, I finally build the password. For all the numbers between 1 and $Length, I'm getting a random item from $arrChars. The result of that is an array, so I use the <em>-join</em> method to create a string from the array. On line 9, I return the password I built.

Here's what the script looks like in action.

<pre class="lang:ps decode:true ">PS C:\&gt; Get-RandomPW
ks1NWkgU4NLmeAv^

PS C:\&gt; Get-RandomPW -Length 10
LMHCLFE2Ds

PS C:\&gt; Get-RandomPW -Length 32
$76Gu3xRD$5GDgwe@nE_Ah#63ZSSd=+W

PS C:\&gt; 1..10 | Foreach-Object { Get-RandomPW -Length 8 }
FtU59d42
dvbpGx9f
&amp;&amp;2&amp;8K=x
@SRK$3m6
57A)*%Pc
RhEHAamX
mTfYV2cB
@h)GR1kb
%tUb^KZD
sxb^bZ)&amp;</pre>

&nbsp;
