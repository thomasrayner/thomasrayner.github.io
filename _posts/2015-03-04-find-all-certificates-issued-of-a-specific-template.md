---
layout: post
title: Find All Certificates Issued Of A Specific Template
date: 2015-03-04 08:30
author: thmsrynr@outlook.com
comments: true
categories: [PKI, pki, PowerShell, powershell, PowerShell ISE, powershell ise]
---
As part of another PowerShell script I'm writing, I needed to get an array of all of the certificates issued in my Enterprise PKI environment by a specific Issuing Certificate Authority (CA) that are of a certain Certificate Template.That doesn't sound like such a tall order. You can launch MMC.exe, add the Certification Authority module, browse the issued certificates and see for yourself the different issued certs and their template.

PowerShell is a bit trickier, though, for a couple reasons. First, you're going to need a PowerShell module to help you with this task. I really like PSPKI (<a title="PSPKI" href="https://pspki.codeplex.com/" target="_blank">available on CodePlex</a>). Install that module and run the command to import the module.

```
import-module -Name pspki\n```

The next tricky thing to keep in mind is that your "CertificateTemplate" attribute on each issued cert doesn't always present itself like you think it should. That's pretty ambiguous so I'll explain more.

In the Certificate Authority MMC, most of the certificates you issue should have a value in the Certificate Template column along the lines of <em>Template Name (OID for the template) </em>where the part in brackets is the unique object identifier (OID) for the template. In the MMC, this information is presented pretty consistently. This isn't really the case for PowerShell.

The following command will get you a list of all the Certificate Templates that have been used to issue certs on your CA <em>as the Certificate Templates are presented in PowerShell</em>.

```
Get-CertificationAuthority -computername ca-name.fqdn.tld | Get-IssuedRequest -property CertificateTemplate | select-object -property CertificateTemplate -unique\n```

The first thing we need to do is get the CA since the <strong>Get-IssuedRequest</strong> cmdlet works with a CA. We get the issued requests (the certificates that have been issued from the CA) while making sure to include the CertificateTemplate property. Then we just select the unique Certificate Templates. Mine returns a mixed list of OIDs and more traditional names - not <em>Name (OID) </em>like we saw in the MMC. Keep this in mind as we continue.

<h2>Back on track, where's my list of certs with a specific template?</h2>

With the above information in mind, we're better armed to get a list of all certs issued by our CA with a specific template. We really only have two steps: 1. Find out how the Certificate Template we're concerned with is represented in PowerShell and 2. Actually get the list of certs with that template.

Task 1 isn't so hard. First, go into the Certification Authority MMC and find a cert with the template you are concerned with. Look at the <em>Issued Common Name</em> column and take note of the value in that column. Then in PowerShell, run this command.

```
Get-CertificationAuthority -computername ca-name.fqdn.tld | Get-IssuedRequest -filter "CommonName -eq TheValueYouSawInMMC" -property CertificateTemplate\n```

Like above, we're getting the CA we're concerned with and getting the issued requests. This time, though, we're not looking to return every cert issued, just the one(s) where the Common Name is the same as the value you saw in the MMC. We also need to make sure to include the CertificateTemplate property because it's not returned by default. Use <em>-property * </em>to get every property back and take a detailed look at a certificate. There are some neat things you can do.

This will get you back a bit of interesting information about the certificate you identified in the MMC as being of the correct template. Specifically, you can see what the value is under the CertificateTemplate property. Maybe it's a friendly name, maybe it's an OID. Either way, that's the value that PowerShell is using to identify that particular template.

Use the above value for the CertificateTemplate in this command.

```
Get-CertificationAuthority -computername ca-name.fqdn.tld | Get-IssuedRequest -property CertificateTemplate | ? { $_.CertificateTemplate -eq "The Certificate Template Value From Above Command" }\n```

We're getting the CA, getting all the issued certs (including those certs' CertificateTemplate property) and filtering where the CertificateTemplate property is equal to the one we found in the last command we ran.

There you go! Export that to a CSV, assign it to a variable. The rest is up to you.
