---
layout: post
title: How To Retrieve A Certificate From Azure Key Vault Via PowerShell
date: 2017-04-12 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, Azure, azure, azure automation, azure key vault, certificates, code signing, DevOps, PKI, pki, PowerShell, powershell, VSTS, vsts]
---
So, you've got a certificate stored in Azure Key Vault that you want to download with PowerShell and use on a computer, or some hosted service. How do you get it and actually use it? Well, here, I'll show you.

<!--more-->

First, you've got to have the Azure PowerShell tools installed and be logged into Azure (or be running in a way where you're already authenticated, like in Azure Automation).

<pre class="lang:ps decode:true">Install-Module -Name AzureRm -Repository PSGallery -Scope CurrentUser -Force
Import-Module AzureRm
Login-AzureRmAccount</pre>

Next, it's time to download the certificate. There are some Azure Key Vault cmdlets built in which, helpfully, do not follow the standard AzureRm naming scheme.

<pre class="lang:ps decode:true">$cert = Get-AzureKeyVaultSecret -VaultName 'My-Vault' -Name 'My-Cert'</pre>

Now, we have to convert the SecretValueText property to a certificate.

<pre class="lang:ps decode:true ">$certBytes = [System.Convert]::FromBase64String($cert.SecretValueText)
$certCollection = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2Collection
$certCollection.Import($certBytes,$null,[System.Security.Cryptography.X509Certificates.X509KeyStorageFlags]::Exportable)</pre>

We can convert the SecretValueText to bytes, and use the X509Certificate2Collection class to convert those bytes to a certificate.

Next, we want to write the certificate to a pfx file on a disk somewhere (preferably to a temp location you can clean up later in the script).

<pre class="lang:ps decode:true ">$protectedCertificateBytes = $certCollection.Export([System.Security.Cryptography.X509Certificates.X509ContentType]::Pkcs12, $password)
$pfxPath = "D:\a\1\temp\ThomasRayner-export.pfx"
[System.IO.File]::WriteAllBytes($pfxPath, $protectedCertificateBytes)</pre>

The first line here exports the certificate and protects it with a password, but where did that come from?! Then it writes the protected bytes to a path on the file system.

So where did that password come from? I'm actually storing that in the Azure Key Vault, too.

<pre class="lang:ps decode:true ">$password = (Get-AzureKeyVaultSecret -VaultName 'My-Vault' -Name 'My-PW').SecretValueText
$secure = ConvertTo-SecureString -String $password -AsPlainText -Force</pre>

Now, I can either refer to that pfx file, or I can import it like this.

<pre class="lang:ps decode:true ">Import-PfxCertificate -FilePath "D:\a\1\temp\ThomasRayner-export.pfx" Cert:\CurrentUser\My -Password $secure</pre>

Make sure you clean up your certs after you're done!
