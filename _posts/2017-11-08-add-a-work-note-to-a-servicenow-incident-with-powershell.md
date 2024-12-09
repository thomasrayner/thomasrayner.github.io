---
layout: post
title: Add A Work Note To A ServiceNow Incident With PowerShell
date: 2017-11-08 08:00
author: thmsrynr@outlook.com
comments: true
categories: [api, api, DevOps, PowerShell, powershell, servicenow, servicenow, web content, web request]
---
I have previously written about <a href="http://www.workingsysadmin.com/get-a-servicenow-user-using-powershell/" target="_blank" rel="noopener">working with the ServiceNow API</a>, and I've continued to use it since my last post on the topic. One of the things that I find myself doing a lot is using PowerShell to add a work note to an incident. Luckily, ServiceNow has an API that you can use to interact with it and do this (among many other things).

<!--more-->

Since I know that all my information is stored in the <em>Incident</em> table, it's not too many steps to get an incident out of ServiceNow if I have the incident number.

```
$user = $Credential.Username
$pass = $Credential.GetNetworkCredential().Password
$base64AuthInfo = [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(("{0}:{1}" -f $user, $pass)))
$headers = New-Object "System.Collections.Generic.Dictionary[[String],[String]]"
$headers.Add('Authorization',('Basic {0}' -f $base64AuthInfo))
$headers.Add('Accept','application/json')
$uriGetIncident = "https://$SubDomain.service-now.com/api/now/table/incident?sysparm_query=number%3D$SNIncidentNumber&amp;sysparm_fields=&amp;sysparm_limit=1"
$responseGetIncident = Invoke-WebRequest -Headers $headers -Method "GET" -Uri $uriGetIncident
$resultGetIncident = ($responseGetIncident.Content | ConvertFrom-Json).Result
```

Assuming I already created a credential object named $Credential to hold my ServiceNow creds, I can add do some encoding to assemble them in a way that I can add them to the header of the request I'm about to make. I'm doing that on the first three lines.

On lines 5 - 7, I'm constructing those headers. So far, I'm following all the PowerShell examples given in the ServiceNow documentation and are similar to my last post on using the ServiceNow API.

Line 9 is where I create the URI for the incident get request. You'll notice I have a variable for both the subdomain (will be unique for your instance of ServiceNow) and the ServiceNow incident number.

Lines 10 and 11 get the incident and parse the results of my request.

Now I can add some work notes.

```
$workNotesBody = @"
{"work_notes":"$Message"}
"@
$uriPatchIncident = "https://$SubDomain.service-now.com/api/now/table/incident/$($resultGetIncident.sys_id)"
$null = Invoke-WebRequest -Headers $headers -Method "PATCH" -Uri $uriPatchIncident -body $workNotesBody
```

On lines 1 - 3, I'm making the body of my patch request, to say that I'm adding the value of $Message into the work_notes field of my incident. Line 5 is where I make the URI for this patch activity, using the sys_id that came out of the get query I performed earlier.

On line 5, I'm muting the output of the web request to add the work notes to the incident. I'm reusing the headers I set up for the get query.
