---
layout: post
title: Dynamically Create Pester Tests For PowerShell
date: 2017-09-20 07:00
author: thmsrynr@outlook.com
comments: true
categories: [DevOps, devops, Pester, pester, PowerShell, powershell]
---
The Pester people don't <em>really</em> recommend this, but, I find it can be really helpful sometimes. What I'm talking about is dynamically creating assertions inside of a Pester test using PowerShell. While I think you should strive to follow best practices, sometimes what's best for you isn't always a best practice, and as long as you know what you're doing, I think you can get away with bending the rules sometimes. Don't tell anyone I said that.

<!--more-->

Say you had a requirement to make sure that a function you wrote performed math, correctly. Maybe it looks like this.

<pre class="lang:ps decode:true">function Get-Square {
    param (
        [int]$Number
    )
    $result = $Number * $Number
    $result
}</pre>

This will just get the square of the number we pass it. Your test might look like this.

<pre class="lang:ps decode:true">describe 'Get-Square' {
    it 'squares 1' {
        Get-Square 1 | Should Be 1
    }

    it 'squares 2' {
        Get-Square 2 | Should Be 4
    }

    it 'squares 3' {
        Get-Square 3 | Should Be 9
    }
}</pre>

This would work. It would test your function correctly, and give you all the feedback you expect. There's another way to do this, though. Check out this next example.

<pre class="lang:ps decode:true ">describe 'Get-Square' {
    $tests = @(
        @(1,1),
        @(2,4),
        @(3,9)
    )
    foreach ($test in $tests) {
        it "squares $($test[0])" {
            Get-Square $test[0] | Should Be $test[1]
        }
    }
}</pre>

This particular example gets more complicated, but shows you what I'm talking about. $tests is an array of smaller arrays where the first number is the number to be squared, and the second number is the answer we expect. Then for each test (array in $tests), I'm generating a new <strong>it</strong> assertion. Neat, right?

Yes, in this particular situation, we ignored Pester test cases, which would have worked here too. This was just a silly example to show how you might tackle this problem differently, or in a situation where test cases wouldn't work for you.
