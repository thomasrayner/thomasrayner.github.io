---
layout: post
title: Display All The Claims For A User Visiting Your .NET Core Azure Web App
date: 2018-05-23 07:30
author: thmsrynr
comments: true
categories: [.NET Core, active directory, Azure, azure, C#, C#, DevOps, identity management, MVC, Razor, Razor, something different, web app]
---
Regular visitors of this blog are used to seeing PowerShell and DevOps content, and this is a little bit of a divergence since it's written in C#, and it's a .NET Core MVC Azure Web App, but if it found itself on my plate, maybe it will find itself on yours. I was tasked with writing an Azure Web App that users would visit, sign into using their Azure Active Directory (ie: "Work or School") account, to test if their Conditional Access and MFA was configured properly. Once logged in, a little information about the user is displayed.

Here's how to pop all the claim information for an authenticated user into a Razor Page.

<!--more-->

I decided to put the whole thing into an HTML table in order to make it a bit more readable. It's kind of a challenge to differentiate between the claim name and the value if they aren't aligned nicely. From there, make sure you're using System.Security.Claims, and you can write yourself this foreach loop.
```
&lt;table&gt;
    @foreach (var claim in ((ClaimsIdentity)User.Identity).Claims)
    {
        &lt;tr&gt;
            &lt;td&gt;@claim.Type&lt;/td&gt;
            &lt;td&gt;@claim.Value&lt;/td&gt;
        &lt;/tr&gt;
    }
&lt;/table&gt;\n```
It's not a big mind blower. This is a .cshtml document, so we can write HTML and mix in some inline C#. Using the <strong>ClaimsIdentity</strong> class, we can write a foreach loop for each claim in the identity of the currently logged in user. This assumes that the user isn't logged in more than once (ie: Facebook and Twitter and Azure AD).

Then I'm making a new row in my table for each claim, and separate cells for the claim type, which is the name of the claim, and the claim value.

Nice and concise!
