---
layout: post
title: Report On Expiring Certs From A Powered Down Certificate Authority
date: 2014-11-12 09:35
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, certificate authority, PKI, pki, PowerShell, powershell, SMA, sma, Windows CA, windows ca]
---
Let's hypothetically say I have an old Windows Server 2003 Intermediate Certificate Authority. Let's also hypothetically say that I already replaced my antiquated Windows Server 2003 PKI infrastructure with a Windows Server 2012 PKI infrastructure and I am only keeping the 2003 stuff around so it can publish a CRL and to run a monthly script that tells me which certs are going to expire within 60 days. It's good to know which certs will expire within 60 days so you can remember to renew them or confirm that they don't need renewal.

Perhaps I decide to shut down the 2003 CA so it quits taking up resources and power but I keep it around in case I need to power it back on and revoke a certificate. <strong>How do I keep getting those monthly reports about which certs will expire soon?</strong> <em>Note: I'm not addressing the CRL publishing concerns or certificate revocation procedure in this post. We're only talking about the expiring soon notification issue.</em>

Service Management Automation to the rescue! We're going to set up an SMA runbook that is going to send us monthly emails about which certs from this 2003 CA are going to expire within 60 days. How the heck are we going to do that when the server is powered off? Well, we're going to cheat.

If we're going to power this CA down, we're going to need to get the information on its issued certificates from somewhere else. A CSV file would be a nice, convenient way to do this. As it would turn out, generating such a CSV file is really easy.

Before you power off the old CA, log into it and open the Certificate Authority MMC. Expand the Certification Authority (server name) tree, and the tree for the name of the CA. You should see Revoked Certificates, Issued Certificates, Pending Requests, Failed Requests and maybe Certificate Templates if you've got an Enterprise PKI solution. Right click on Issued Requests and click Export List. Switch the Save As Type to CSV and put the file somewhere that you can see it from within Service Management Automation like a network share. <em>Note: Once I get my CSV out of the CA MMC, I manually removed the white space out of the column headings to make it nicer for me to read.</em>

[caption id="attachment_42" align="aligncenter" width="300"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2014/11/11-10-2014-9-55-35-AM.png"><img class="wp-image-42 size-medium" src="http://www.workingsysadmin.com/wp-content/uploads/2014/11/11-10-2014-9-55-35-AM-300x178.png" alt="" width="300" height="178" /></a> Export your list of Issued Certificates to a CSV file.[/caption]

Now the fun part. Time to put together an SMA runbook that will go through this CSV and email me a list of all the certs that are going to expire within 60 days of the current date. Sounds scary right? Well it turns out that it isn't so bad.

Let's start simply by initializing our PowerShell Workflow. You get to this point in SMA by creating a new runbook. I'm also going to set up a whopping one variable.

<pre class="wrap:true lang:ps decode:true ">workflow GetExpiringCerts
{
    $strInPath = Get-AutomationVariable -Name 'INFOLDER'
}</pre>

Our workflow/runbook is called GetExpiringCerts. The variable $strInPath is the location to where I have all the files I ever load into SMA. That is, it's just a path to a network share that's the same in all my runbooks that use it.

So far so good? Good. Next we need to look through the CSV that's somewhere beneath $strInPath for all our certs. Let's break down that big block of code:

<pre class="wrap:true lang:ps mark:4-10 decode:true">workflow GetExpiringCerts
{
    $strInPath = Get-AutomationVariable -Name 'INFOLDER'
    $strCerts = inlinescript { 
        $csvCerts = import-csv "$using:strInPath\GETEXPIRINGCERTS\IssuingCA.csv"
        $arrCertsExpireAfterToday = $csvCerts | ? { (get-date -date $_.CertificateExpirationDate) -ge (get-date) } | ? { (get-date -date $_.CertificateExpirationDate) -le (get-date).addmonths(2) }
        $strResults = "Certificates expiring on NAME OF YOUR CA"
        $arrCertsExpireAfterToday | % { $strResults += "&lt;br&gt;&lt;br&gt;"; $strResults += "&lt;b&gt;Issued Common Name:&lt;/b&gt; " + $_.IssuedCommonName; $strResults += "&lt;br&gt;&lt;b&gt;Expires:&lt;/b&gt; " + $_.CertificateExpirationDate; $strResults += " &lt;b&gt;Requested By:&lt;/b&gt; " + $_.RequesterName }
        $strResults
    }
}</pre>

There's some cheating right there. PowerShell Workflows are different than regular vanilla PowerShell in ways that I don't always like. To make a PowerShell Workflow (which is what SMA runbooks use) execute some code like regular PowerShell, you need to wrap it in an <strong>inlinescript</strong> block. We're going to take the output of the inline script and assign it to $strCerts.

Let's break down what's inside that inlinescript block. First we're going to import the CSV full of our Issued Certificates from the CA. To use a variable defined outside the inlinescript, you prefix it with "using:", hence $using:strInPath. $strInPath is defined outside the inlinescript block but I want to use it inside the inlinescript block.

Now to build an array of all the certs we care about. The variable $arrCertsExpireAfterToday is going to hold a selection of the CSV we loaded into $csvCerts. We take $csvCerts and pipe it into a few filters. The first: where the Certificate Expiration Date is greater than today's date. That way we don't look at any certs that are already expired. The second: where the Certificate Expiration Date is less than two months from now. That way we don't see certs that expire in two years that we don't care about yet. That's it! That's the array of certs. Now all we need to do is make the output look nice and send it.

On line 7, we start building the body of the email we're going to send and assigning the future body of our email to $strResults. I want to send an HTML email because it's prettier. My email will start with a line that tells us what's coming next. Then, we need to get the information out of $arrCertsExpireAfterToday and format it nicely so it may be sent. We're going to pipe the contents of $arrCertsExpireAfterToday through a foreach-object function that will make some nice HTML output containing the Issued Common Name, the Certificate Expiratino Date and the Requester Name. You can format your report differently, take different headings, etc., but this is what worked for me.

I print $strResults on line 9, as the last thing I do in the inlinescript block so that $strResults becomes the value returned by the inlinescript block and therefore the value of $strCerts (line 4).

We're almost out of the woods. All we have to do now is send the email.

<pre class="wrap:true lang:ps mark:12-15 decode:true ">workflow GetExpiringCerts
{
    $strInPath = Get-AutomationVariable -Name 'INFOLDER'
    $strCerts = inlinescript { 
        $csvCerts = import-csv "$using:strInPath\GETEXPIRINGCERTS\IssuingCA.csv"
        $arrCertsExpireAfterToday = $csvCerts | ? { (get-date -date $_.CertificateExpirationDate) -ge (get-date) } | ? { (get-date -date $_.CertificateExpirationDate) -le (get-date).addmonths(2) }
        $strResults = "Certificates expiring on NAME OF YOUR CA"
        $arrCertsExpireAfterToday | % { $strResults += "&lt;br&gt;&lt;br&gt;"; $strResults += "&lt;b&gt;Issued Common Name:&lt;/b&gt; " + $_.IssuedCommonName; $strResults += "&lt;br&gt;&lt;b&gt;Expires:&lt;/b&gt; " + $_.CertificateExpirationDate; $strResults += " &lt;b&gt;Requested By:&lt;/b&gt; " + $_.RequesterName }
        $strResults
    }
     
    $strSubject = "The following certificates expire on Cora in less than two months"
    $strEmail = @("ThmsRynr@outlook.com","other@people.com")
    $strSMTPServer = Get-AutomationVariable -Name 'SMTPServer'
    send-mailmessage -to $strEmail -From "service_account@yourdomain.com" -Subject $strSubject  -SMTPServer $strSMTPServer -body $strCerts -bodyashtml
}</pre>

Easy. We need a subject, a list of people to send the email to, and an SMTP server. My email To list is an array and I store my SMTP server in an SMA asset. Then I use the send-mailmessage cmdlet to shoot this email off. Make sure to use the <strong>-bodyashtml</strong> flag so the HTML is parsed correctly instead of being included as plaintext.

That's it! Set an SMA schedule to run monthly and you'll get yourself monthly email notifications of certificates that are due to expire within 60 days even though the CA that issued them is powered off!
