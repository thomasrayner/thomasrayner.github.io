---
layout: post
title: Getting Started With Pester
date: 2016-06-22 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Pester, pester, PowerShell, powershell, PowerShell 5.0, powershell 5.0, powershell gallery]
---
If you don't know what Pester is, it's a <a href="https://github.com/pester/Pester" target="_blank">framework for running unit tests and validating PowerShell code</a>. Also, it's awesome. In May I finally dipped my toe in the water with a pretty simple test for a REALLY simple function. I'm not going to go into a world of detail on how exactly all my Pester code works because there are tons of <a href="http://www.powershellmagazine.com/2014/03/12/get-started-with-pester-powershell-unit-testing-framework/" target="_blank">guides for that</a>. What I'm going to do instead is provide a quick run down of what I came up with.

First things first, I need a function to validate.

<pre class="lang:ps decode:true ">function Write-SomeMath 
{
    param(
        [int]$First,
        [int]$Second
    )
    return $First + $Second
}</pre>

I guess that will work. <strong>Write-SomeMath</strong> takes two integers and returns their sum. Hardly a breathtaking display of complexity and function but it will do just fine for this example.

Now I need to install Pester. The easiest way to do this is using the <strong>PSGet</strong> module in PowerShell 5.0 to get it from <a href="http://powershellgallery.com" target="_blank">PowerShellGallery.com</a>.

<pre class="lang:ps decode:true ">Install-Module Pester -Scope CurrentUser -Force
Import-Module Pester</pre>

The next thing I need is a <em>Describe</em> block.

<pre class="lang:ps decode:true ">Describe 'GoofingWithPester.ps1' {

}</pre>

This <em>Describe</em> block will contain and - you guessed it - describe the tests (I just used my filename) and provide a unique TestDrive (check out the getting started link).

Now I need a <em>Context </em>block.

<pre class="lang:ps mark:2-4 decode:true">Describe 'GoofingWithPester.ps1' {
    Context 'Write-SomeMath' {
        
    }
}</pre>

I'm further grouping my tests by creating a <em>Context</em> here for my <strong>Write-SomeMath</strong> function. This could have been named anything.

Now, I could start with a bunch of tests, but I want to show off a particular feature of Pester that allows you to pass an array of different test cases.

<pre class="lang:ps mark:3-22 decode:true">Describe 'GoofingWithPester.ps1' {
    Context 'Write-SomeMath' {
        $testcases = @(
            @{
                fir  = 1
                sec  = 2
                exp  = 3
                test = '1 and 2'
            }, 
            @{
                fir  = 3
                sec  = 6
                exp  = 91 #wrong on purpose
                test = '3 and 6 (wrong on purpose)'
            }, 
            @{
                fir  = 4
                sec  = 6
                exp  = 10
                test = '4 and 6'
            }
        )

    }
}</pre>

All I did was define an array called <em>$testcases</em> which holds an array of hash tables. It's got the first number, second number, expected result and a name of what we're testing. Now I can pass this entire array to a test rather than crafting different tests for all of them individually.

<pre class="lang:ps mark:23-26 decode:true">Describe 'GoofingWithPester.ps1' {
    Context 'Write-SomeMath' {
        $testcases = @(
            @{
                fir  = 1
                sec  = 2
                exp  = 3
                test = '1 and 2'
            }, 
            @{
                fir  = 3
                sec  = 6
                exp  = 91 #wrong on purpose
                test = '3 and 6 (wrong on purpose)'
            }, 
            @{
                fir  = 4
                sec  = 6
                exp  = 10
                test = '4 and 6'
            }
        )
        It 'Can add &lt;test&gt;' -TestCases $testcases {
            param($fir,$sec,$exp)
            Write-SomeMath -First $fir -Second $sec | Should Be $exp
        }

    }
}</pre>

This is an <em>It</em> block which is what Pester calls a test. I've named it "Can add &lt;test&gt;" and it will pull the "test" value from the hashtable and fill it in. Cool! I'm using the <em>-TestCases</em> parameter to pass my array of test cases to the <em>It</em> block. Then I've got parameters inside the test for my first value, second value and expected outcome. I execute <strong>Write-SomeMath</strong> with the values pulled from my test cases and pipe the result to "<strong>Should Be</strong>" to compare the outcome to my expected outcome.

Now, just one more test for fun. What if I don't pass an integer to my function?

<pre class="lang:ps mark:27-29 decode:true ">Describe 'GoofingWithPester.ps1' {
    Context 'Write-SomeMath' {
        $testcases = @(
            @{
                fir  = 1
                sec  = 2
                exp  = 3
                test = '1 and 2'
            }, 
            @{
                fir  = 3
                sec  = 6
                exp  = 91 #wrong on purpose
                test = '3 and 6 (wrong on purpose)'
            }, 
            @{
                fir  = 4
                sec  = 6
                exp  = 10
                test = '4 and 6'
            }
        )
        It 'Can add &lt;test&gt;' -TestCases $testcases {
            param($fir,$sec,$exp)
            Write-SomeMath -First $fir -Second $sec | Should Be $exp
        }
        It 'Detects wrong datatypes' {
            {Write-SomeMath -First 9 -Second 'cat'} | Should throw
        }
    }
}</pre>

Another <em>It</em> block for detecting wrong datatypes. I pipe the result into <strong>Should throw</strong> because my function should throw an error. For this to work properly, the code I'm testing has to be wrapped in a scriptblock, otherwise the thrown error will occur and be trapped in my function.

Here's the outcome when I run this file!

[caption id="attachment_355" align="alignnone" width="838"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2016/05/2016-05-19-13_55_30-Cortana.png"><img class="size-full wp-image-355" src="http://www.workingsysadmin.com/wp-content/uploads/2016/05/2016-05-19-13_55_30-Cortana.png" alt="Getting Started With Pester - Results" width="838" height="168" /></a> Pester Results[/caption]

Pretty cool. My first test passes, the second one fails and tells me why, the third and fourth tests pass. The fourth one is especially interesting. The function FAILED but because the test said it SHOULD FAIL, the test itself passed.

So that's my "dip my toes in the water" intro Pester test. Stay tuned for more complicated examples.
