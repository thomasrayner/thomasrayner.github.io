---
layout: post
title: My August 2015 Scripting Puzzle Solution
date: 2015-08-04 08:19
author: thmsrynr@outlook.com
comments: true
categories: [json, mvp, mvp, PowerShell, powershell, powershell.org, Scripting Puzzle, scripting puzzle, scriptingpuzzle, web reqeuest]
---
If you haven't heard, PowerShell.org is taking the lead on organizing the PowerShell Scripting Games. There's a new format that involves monthly puzzles. Here's their post on August's puzzle: <a href="http://powershell.org/wp/2015/08/01/august-2015-scripting-games-puzzle/" target="_blank">http://powershell.org/wp/2015/08/01/august-2015-scripting-games-puzzle/</a>

Here is my solution. The instructions are to get information back from a JSON endpoint (read more about it in the link above).

First things first, here's how I did the one-liner part.

```
Invoke-WebRequest http://www.telize.com/geoip | ConvertFrom-Json | Format-Table Longitude,Latitude,Continent_Code,Timezone -AutoSize
```

This brings back exactly what Mr. Don Jones has asked for. I'm using the <strong>Invoke-WebRequest</strong> cmdlet to make a web request to that IP and converting what's returned using <strong>ConvertFrom-Json. </strong>Then it's just a matter of formatting the output and selecting only the items we care about for this puzzle.

Alright, that wasn't so bad. How about the next challenge? I wrote the following function.They asked for <a href="https://technet.microsoft.com/en-us/magazine/hh360993.aspx" target="_blank">an advanced function</a>, but I skipped the comment based help and the begin/process blocks. I could clean up how I work with the $IP parameter a bit, but, this is easier to look at and explain.

```
function Get-GeoIP
{
    param
    (
        [array]$Attributes = '*',
        [IPAddress]$IP
    )
    Try
    {
        if ($IP) { Invoke-WebRequest "http://www.telize.com/geoip/$IP" | ConvertFrom-Json | Select-Object $Attributes }
        else { Invoke-WebRequest 'http://www.telize.com/geoip' | ConvertFrom-Json | Select-Object $Attributes }
    }
    
    Catch [Exception]
    {
        throw $_.Exception.Message
    }
}
```

I've declared two parameters, $Attributes and $IP. $Attributes are the attributes we want to return. In our puzzle instructions, we're asked for Longitude, Latitude, Continent_Code and Timezone but you could use this function to get any of them. By default, the function will return all attributes. $IP is another IP address that we can get data for. If you don't specify one, the function will retrieve data for the client's IP. Otherwise, we can get data for an IP that isn't the one we're making our request from.

Here are a couple examples of the function in action.

```
PS C:\&gt; Get-GeoIP


longitude      : redacted
latitude       : redacted
asn            : redacted
offset         : redacted
ip             : redacted
area_code      : 0
continent_code : NA
dma_code       : 0
city           : Edmonton
timezone       : America/Edmonton
region         : Alberta
country_code   : CA
isp            : redacted
postal_code    : redacted
country        : Canada
country_code3  : CAN
region_code    : AB
```

Here, I'm just running the script with no parameters set. It gets all the data back from my IP. I've sanitized a lot of the data returned for the purpose of publishing this post but it was all returned correctly.

```
PS C:\&gt; Get-GeoIP -Attributes @('Longitude','Latitude','Continent_Code','Timezone') -IP 104.28.14.25 | Format-Table -AutoSize

longitude latitude continent_code timezone           
--------- -------- -------------- --------           
-122.3933  37.7697 NA             America/Los_Angeles
```

Here, I asked for the attributes from the puzzle and specified the IP address for <a href="http://powershell.org" target="_blank">PowerShell.org</a>. You can see that it returned exactly what we'd expect.

Finally, the challenge asks us to hit another public JSON endpoint. I don't have a favorite but found one that shows you your <a href="http://headers.jsontest.com/" target="_blank">HTTP request information</a>. Here is what it looks like in action.

```
PS C:\&gt; Invoke-WebRequest 'http://headers.jsontest.com/' | ConvertFrom-Json | Format-Table -AutoSize

Host                 User-Agent                                                           
----                 ----------                                                           
headers.jsontest.com Mozilla/5.0 (Windows NT; Windows NT 6.2; en-US) WindowsPowerShell/4.0
```

Interesting user agent.
