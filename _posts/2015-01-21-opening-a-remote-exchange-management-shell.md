---
layout: post
title: Opening A Remote Exchange Management Shell
date: 2015-01-21 01:45
author: thmsrynr@outlook.com
comments: true
categories: [Exchange, exchange, PowerShell, powershell, PowerShell ISE, powershell ise]
---
Here's a function I stuck in my PowerShell profile. I found myself making lots of remote connections to my Exchange 2013 environment so I put together a quick function to create the connection for me. It's far from perfect but it saves me time every single time I use it so check it out.

```
function gimme-exchange ()
{
    $arrExchangeServersURI = @("http://fqdn-of-server-one/Powershell","http://fqdn-of-server-two/Powershell")
    $success = $false
    $UserCredential = Get-Credential
    ForEach ($connectionURI in $arrExchangeServersURI)
    {
        Try
        {
            If($success -ne $true)
            {
                $getMBXconn = new-pssession -configurationname Microsoft.Exchange -connectionuri $connectionURI -Authentication Kerberos -Credential $UserCredential
                $null = Import-PSSession -AllowClobber $getMBXConn
                $success = $true
            }
        }
        catch [Exception]
        {
            $strError = $_.Exception.Message
            $strError = "Error: ${strError}"
            $success = $false
        }
    }
}
```

On Line 1, we're declaring the function - no big deal. I'm naming mine "gimme-exchange" so once my profile loads, I can just type that to start the function.

On Lines 3 to 5 I'm setting a few variables. Line 3 is weird. I made an array of the different Exchange servers I had rather than going through some autodiscovery process. The script will try to open a connection to the first one, if it fails, try the second one, and so on. It's inefficient but I don't add and remove a lot of Exchange servers so I can get away with it since this function is just for me. Line 4 is going to be used to detect if we made a connection or not. Line 5 will prompt and store the administrative credentials that you will use to create the connection.

On Line 6, we start looping through all the servers I specified in Line 3. In a Try/Catch block, if we haven't already made a successful connection to a previous Exchange server, we're going to make a new connection and import it. You have to make sure you use the -configurationname item because we're not just creating any old PSSession, Exchange is funny and we connect to it using some special parameters shown in Line 12. When we import the session on Line 13, we're going to allow clobbering of other existing cmdlets and suppress the output of the import command.

If we run into an error anywhere in the Try block, the Catch block is setup to echo out the error message and continue looping through servers depending on how severe the error is.

That's it! Yay, saving time.

<hr />

<strong>Update:</strong> If you're already logged in as the user you want to connect to Exchange as, you can skip the credential gathering part and run this instead.

```
$arrExchangeServersURI = @("http://fqdn-of-server-one/Powershell","http://fqdn-of-server-two/Powershell")
$success = $false
ForEach ($connectionURI in $arrExchangeServersURI)
{
    Try
    {
        If($success -ne $true)
        {
            $getMBXconn = new-pssession -configurationname Microsoft.Exchange -connectionuri $connectionURI -Authentication Kerberos
            $null = Import-PSSession -AllowClobber $getMBXConn | Out-null
            $success = $true
        }
    }
    catch [Exception]
    {
        $strError = $_.Exception.Message
        $strError = "Error: ${strError}"
        $success = $false
    }
}
```

&nbsp;
