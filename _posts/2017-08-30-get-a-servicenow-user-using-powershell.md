---
layout: post
title: Get A ServiceNow User Using PowerShell
date: 2017-08-30 07:00
author: thmsrynr@outlook.com
comments: true
categories: [api, api, PowerShell, powershell, servicenow, servicenow]
---
ServiceNow is a cloud computing company whose software is used for IT Service Management based on ITIL standards. They've got a bunch of different modules for managing problems and incidents, operations management, performance analytics, and more. You there some custom development you can do to modify their solutions or build your own. It's pretty flexible, and we use it where I work.

I have been working with the ServiceNow API a lot lately. This week, I'm going to show you something pretty simple: Getting a ServiceNow user.

Let's jump into some code first and I'll break down what I'm doing.

<strong><!--more--></strong>

```
$Credential = Get-Credential
$SubscriptionSubDomain = 'mysub'
$Username = 'thmsrynr'

$user = $Credential.Username
$pass = $Credential.GetNetworkCredential().Password
$base64AuthInfo = [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(("{0}:{1}" -f $user, $pass)))

$headers = New-Object "System.Collections.Generic.Dictionary[[String],[String]]"
$headers.Add('Authorization',('Basic {0}' -f $base64AuthInfo))
$headers.Add('Accept','application/json')

$uri = "https://$SubscriptionSubDomain.service-now.com/api/now/v1/table/sys_user?sysparm_query=user_name=$Username"

$response = Invoke-WebRequest -Headers $headers -Method "GET" -Uri $uri 
$result = ($response.Content | ConvertFrom-Json).Result
```

First, I'm compiling the authentication information and header info as per the ServiceNow documentation. This isn't my favorite way of handling credentials, but it's what the ServiceNow documentation recommends and, well, it works.

Next, I'm constructing my URI using a variable holding my subdomain and another variable for the username I'm interested in ($SubscriptionSubDomain and $Username respectively).

Then, I am invoking the web request to get the information about the user, and parsing the result. I can then use the $result variable later in my script.

This has been particularly helpful for me when I'm trying to figure out the sys_id (ServiceNow's unique ID) for a specific user and all I know is their username.
