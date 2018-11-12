---
layout: post
title: Editing An Azure DevOps Build Definition From Within The Build
date: 2018-09-19 07:30
author: thmsrynr
comments: true
categories: [Automation, Azure, azure, azure devops, azure devops, DevOps, devops, PowerShell, powershell, VSTS, vsts]
---
It's been a little while since I've managed to get a blog post out! Not to worry, though, as <a href="https://workingsysadmin.com/i-was-re-awarded-as-a-microsoft-mvp-but-im-leaving-the-program/" target="_blank" rel="noopener">I've been nice and busy</a>. One of the things I've been working on lately is writing a VSTS- I mean Azure DevOps extension.

The extension I'm working on will, among other things, need to update the build definition of the build that it's currently building. Why? Because I'm incrementing a version number that's stored in a build variable, which is part of the build definition. Here's how I'm doing it.

<!--more-->

First, you need to make sure that you grant the build permissions to access the OAuth key. This is under the additional options section of the agent job configuration. Then it's time for some code.
<pre class="lang:default decode:true">$personalAccessToken = $env:system_accesstoken
$headers = @{"Authorization" = "Bearer $personalAccessToken"}
$headers.Add("Content-Type", "application/json")
        
$getBuildUri = "$($env:SYSTEM_TEAMFOUNDATIONSERVERURI)$($env:SYSTEM_TEAMPROJECT)/_apis/build/builds/$($env:BUILD_BUILDID)?api-version=4.1"
$getBuildResponse = Invoke-RestMethod -Uri $getBuildUri -Headers $headers

$getVarsUri = "$($env:SYSTEM_TEAMFOUNDATIONSERVERURI)$($env:SYSTEM_TEAMPROJECT)/_apis/build/definitions/$($getBuildResponse.Definition.Id)?api-version=4.1"
$getVarsResponse = Invoke-RestMethod -Uri $getVarsUri -Headers $headers</pre>
First, I'm retrieving the access token, and building the authorization and content-type elements of the headers that I'm going to use to interact with the Azure DevOps API. Then, I'm going to get the build definition for the build that's currently running. After that, I'll get the definition for that build.

Then, I need to edit the variable that I want to manipulate, and write it back to Azure DevOps.
<pre class="lang:default decode:true">$getVarsResponse.variables.$Variable.value = $newValue
    
$putData = $($getVarsResponse | ConvertTo-Json -Compress -Depth 10)
$null = Invoke-RestMethod -Uri $getVarsUri -Method PUT -Body $putData -Headers $headers</pre>
In this example, $Variable is the name of the build variable whose value I want to edit. Then I'll convert the PowerShell object back to JSON, and put it back in Azure DevOps.

Once you do this, it takes a few seconds for what you did in via the API to be reflected in the web portal you access through the browser. Sometimes you have to wait a minute or two to make sure your change actually took place.

A big thanks to <a href="https://twitter.com/HalbaradKenafin" target="_blank" rel="noopener">Chris "Halbarad" Gardner</a> for helping me negotiate some challenges as I worked on this.

&nbsp;
