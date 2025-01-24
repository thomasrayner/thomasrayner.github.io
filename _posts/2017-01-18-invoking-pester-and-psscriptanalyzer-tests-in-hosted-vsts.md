---
layout: post
title: Invoking Pester and PSScriptAnalyzer Tests in Hosted VSTS
date: 2017-01-18 08:30
author: thmsrynr@outlook.com
comments: true
categories: [DevOps, devops, Pester, pester, PowerShell, powershell, pssa, PSScriptAnalyzer, psscriptanalyzer, release management, release pipeline, testing, testing, unit testing, VSTS, vsts]
---
<h1><a name="_Toc469997945"></a>Overview</h1>

Pester and PSScriptAnalyzer are both fundamental tools for testing the effectiveness and correctness of PowerShell scripts, modules, and other PowerShell artifacts. While it is relatively convenient and straightforward to run these tools on a local development workstation, and even on owned/on-prem testing servers, it is somewhat more complicated to execute these tests in your own Microsoft-hosted Visual Studio Team Services environment.

Pester is an open source domain specific language developed originally by Dave Wyatt, which enjoys contributions from a variety of prominent members of the PowerShell community, as well as Microsoft employees on the PowerShell product team. Microsoft is a big enough fan of Pester that it comes with Windows 10, and reference it frequently in talks and written material. Pester is used for PowerShell unit testing.

PSScriptAnalyzer is a static code checker for PowerShell modules and scripts that checks the quality of code by comparing it against a set of rules. The rules are based on PowerShell best practices identified by the PowerShell team at Microsoft and the community. It is shipped with a collection of built-in rules but supports the ability to include or exclude specific rules, and also supports custom rule definitions. PSScriptAnalyzer is an open source project developed originally by the PowerShell team at Microsoft.

Lots of DevOps teams use the above tools together, along with their internally generated standards and style guide, to ensure that PowerShell code that is released into any environment meets their standards. By using Pester to ensure that a piece of code performs the tasks required, using PSScriptAnalyzer to inspect code for general best practice violations, and using a peer review process to validate that code conforms to our standards and style guidelines, you can rigorously test and ensure the quality and functionality of all PowerShell code that you produce.

As part of a PowerShell Release Pipeline, you may store your code in the source control portion of VSTS, hosted by Microsoft. I'd suggest you use the automated build and release components of VSTS to execute a series of tasks before deploying, and to deploy PowerShell code. Two of these tasks are running Pester tests and PSScriptAnalyzer. As a standard, don't release builds if any part of either of these two tests fail.

In previous versions of VSTS, the hosted build service ran PowerShell 4.x. Because installing modules from the PowerShell Gallery (to get Pester and PSScriptAnalyzer module files so they may be run) requires PowerShell 5.0 or higher, it was necessary to use a third-party configured build step or perform some other hijinks that possibly compromised the integrity of a build. Now that VSTS runs PowerShell 5.0, we can run Pester, PSScriptAnalyzer, and many other helpful modules without exporting them with our other code, or using third-party build steps.

<!--more-->

<h1><a name="_Toc469997946"></a>Prerequisites</h1>

Before following the steps in this guideline, there are several prerequisites and assumptions regarding access, knowledge, and already produced artifacts.

<ol>
    <li>Access to VSTS and permission to create builds in whichever area you are working in</li>
    <li>Know how to use Pester and PSScriptAnalyzer on local workstation</li>
    <li>Have produced Pester tests, and if applicable, custom PSScriptAnalyzer rule files</li>
    <li>Have a PowerShell script or module to test</li>
</ol>

<h1><a name="_Toc469997947"></a>Preparing Artifacts</h1>

PowerShell scripts and modules should be stored in a separate file from the tests that are run to validate their functionality. Typically, within a root folder, you will have a ModuleName (or ScriptName) folder which contains all of the .ps1, .psm1, .psd1, .dll, etc. files and artifacts that must be deployed for the code to be functional. Since tests are not deployed along with the rest of the functional artifacts, they should be stored in a Tests folder in the root module, at the same level as the ModuleName folder.

All of the above should be saved in VSTS source control.

<h2><a name="_Toc469997948"></a>The execution script (Invoke-Test.ps1)</h2>

It is assumed, above, that you have written Pester tests for your code, that the Pester tests have gone through peer review, and were determined to be complete and thorough. It is also assumed that they are stored as described in the standards and style guideline document.

Although the test results from Pester and PSScriptAnalyzer are separate and independent, because of the overhead of loading all of the required modules, it makes more sense to simply use one script to load the required modules and us it to call all of the different tests.

The script inside <em>Invoke-Test.ps1</em> should look something like this.

```
$ErrorActionPreference = 'stop'
Install-PackageProvider -Name Nuget -Scope CurrentUser -Force -Confirm:$false
Install-Module -Name Pester -Scope CurrentUser -Force -Confirm:$false
Install-Module -Name PSScriptAnalyzer -Scope CurrentUser -Force -Confirm:$false
Import-Module Pester
Import-Module PSScriptAnalyzer
Invoke-Pester -OutputFile 'PesterResults.xml' -OutputFormat 'NUnitXml' -Script '.\Tests\Set-E.tests.ps1'
Invoke-Pester -OutputFile 'PSSAResults.xml' -OutputFormat 'NUnitXml' -Script '.\Tests\PSSA.tests.ps1'
```

Broken down line by line, the script performs the following tasks.

<ol>
    <li>Sets the ErrorActionPreference to stop. In this instance, we want any error thrown to be a terminating error and setting the ErrorActionPreference is the most convenient way to achieve this (it isn’t 100% effective, but works for this purpose). Normally, we wouldn’t want to perform such a significant change to a user’s working environment, but VSTS testing environments are ephemeral and therefore won’t be around after we’re done testing to experience any consequences.</li>
    <li>Installs Nuget as a package provider. The following two lines install modules from the PowerShell Gallery (powershellgallery.com) and the first time you try to do that, PowerShell will prompt you to accept the installation of Nuget. In the non-interactive hosted VSTS test environment this is not possible and so line number 2 performs this task proactively.</li>
    <li>Installs Pester from the PowerShell Gallery. This has to be for the scope <em>CurrentUser</em> because the test user running the code is not an administrative one.</li>
    <li>Installs PSScriptAnalyzer from the PowerShell Gallery. This also needs to be for the <em>CurrentUser</em> scope for the same reason as line 3.</li>
    <li>Imports the Pester module into the test user’s session.</li>
    <li>Imports the PSScriptAnalyzer module into the test user’s session.</li>
    <li>Runs the Pester test associated with this script or module and outputs the results in an XML document formatted as NUnitXML so VSTS can pick it up later.</li>
</ol>

You may have several different Pester tests for a script or module and so you may want to add some logic to this line to loop through a bunch of different tests, or simply repeat the same line more than once. It is important that you generate a unique XML file for each test you run to avoid overwriting the results of one test with another.

<ol start="8">
    <li>Runs the PSScriptAnalyzer test. This looks like another Pester test, because it technically is. We use Pester as sort of a wrapper around a PSScriptAnalyzer test.</li>
</ol>

By default, PSScriptAnalyzer will dump its results to a user’s console window, because it’s made primarily to be an interactive tool. There are different solutions for using PSScriptAnalyzer as an unattended solution, and this is one of them.

<h2><a name="_Toc469997949"></a>Pester tests (*.tests.ps1)</h2>

Testing logic and standards are not covered at this time in this guide. There are numerous PluralSight courses, books, and online resources for learning proper testing methodology and learning how Pester works. Keep in mind while writing Pester tests that the module you are testing is in a different location than the test is located (if you are following the recommended standards and style). So, to dot-source a script within a test, you may need to reference a location like <em>..\ScriptName\Script-Name.ps1</em>.

Confirm the functionality of your tests on your local workstation before following the steps in this guide. It is much easier to troubleshoot a faulty test in your local environment than it is to do so in a hosted VSTS build environment.

<h2><a name="_Toc469997950"></a>PSScriptAnalyzer tests (PSSA.tests.ps1)</h2>

The script for running PSScriptAnalyzer in hosted VSTS is more clearly defined than the Pester tests, addressed above. This guide does not cover the inclusion or exclusion of specific rules, or the use of custom rules. The majority of PowerShell code tested will be well served by the standard rule configuration that comes with PSScriptAnalyzer. If you are looking to use custom rule sets, it is assumed that you will be capable of altering the below script to suit your unique needs.

The Pester test that runs PSScriptAnalyzer testing should look something like this.

```
Describe 'Testing against PSSA rules' {
       Context 'PSSA Standard Rules' {
        $analysis = Invoke-ScriptAnalyzer -Path '..\ScriptName\Set-E.ps1'
        $scriptAnalyzerRules = Get-ScriptAnalyzerRule

        forEach ($rule in $scriptAnalyzerRules) {
            It "Should pass $rule" {
                If ($analysis.RuleName -contains $rule) {
                    $analysis |
                         Where RuleName -EQ $rule -outvariable failures |
                         Out-Default
                    $failures.Count | Should Be 0
                }
            }
        }
    }
}
```

The basic logic of this Pester test is that it performs an <em>Invoke-ScriptAnalyzer</em> on the script we are interested in testing (this may need to be adjusted for your purposes to include all of the files associated with a module, etc.), and examines the results. The script gets a list of all of the PSScriptAnalyzer rules, writes a test for each rule, and if the analysis contains any of the rules, the test for that specific rule is violated. Running the tests this way allows us to export granular results that indicates which PSScriptAnalyzer rule was broken from within VSTS.

<h1><a name="_Toc469997951"></a>Configuring the VSTS Build</h1>

Normally when you configure a VSTS build for a PowerShell script or module, you will also have steps for signing the artifacts, some other tests for business validation, and perhaps some other preparation for a VSTS release. In this guideline, we are concerned only with the Pester and PSScriptAnalyzer testing and so this build will look otherwise incomplete.

<h2><a name="_Toc469997952"></a>Steps</h2>

<ol>
    <li>Create a new build in the appropriate folder</li>
    <li>Add two build steps
<ol>
    <li>Run a PowerShell script</li>
    <li>Publish test results</li>
</ol>
</li>
    <li>Configure the “Run a PowerShell script” step
<ol>
    <li>Give a more meaningful name such as “Run Pester &amp; PSSA Tests”</li>
    <li>Type: File Path</li>
    <li>Script Path: Identify the <em>Invoke-Test.ps1</em> file which operates as per above section</li>
    <li>Arguments: Leave blank</li>
    <li>Advanced
<ol>
    <li>Working folder: Change to the root folder for the module or script <u>(Important)</u></li>
    <li>Fail on Standard Error: Checked</li>
</ol>
</li>
    <li>Control Options
<ol>
    <li>Enabled: Checked</li>
    <li>Continue on error: Checked</li>
</ol>
</li>
    <li>Always run: Checked</li>
    <li>Timeout: 0</li>
</ol>
</li>
</ol>

<ol start="4">
    <li>Configure the “Publish test results” step
<ol>
    <li>Test Result Format: NUnit</li>
    <li>Test Results Files: **/*Results.xml (Important: whatever this pattern is, <u>all the XML documents</u> you configure in the last few lines of <em>Invoke-Test.ps1</em> need to match the pattern)</li>
    <li>Merge Test Results: Unchecked</li>
    <li>Test Run Title: Leave blank</li>
    <li>Advanced
<ol>
    <li>Platform: Leave blank</li>
    <li>Configuration: Leave blank</li>
    <li>Upload Test Attachments: Checked</li>
    <li>Control Options
<ol>
    <li>Enabled: Checked</li>
    <li>Continue on error: Unchecked</li>
</ol>
</li>
</ol>
</li>
    <li>Always run: Checked</li>
    <li>Timeout: 0</li>
</ol>
</li>
</ol>

<ol start="5">
    <li>Save the build with a meaningful name</li>
    <li>Queue a new build to test your work</li>
</ol>

<h1><a name="_Toc469997953"></a>Looking at Test Results</h1>

After a build has run, if you properly configured the tests as described above, you will be able to view the test results directly in VSTS. Follow these steps to access test results.

<ol>
    <li>Open VSTS</li>
    <li>Enter the Build &amp; Release area</li>
    <li>Navigate to and click the build you are interested in</li>
    <li>You will see a list of recently completed builds in the summary pane, click the interesting one</li>
    <li>Click Tests</li>
</ol>

Here, you’ll see a summary of all of the tests than ran on your code. You’ll see the total tests, failed tests, pass percentage, and how long testing took. You can configure this view a bit, but to see more in depth information about a specific test, click it. All tests are labeled as Pester tests, because they technically are (recall, we used Pester to identify PSScriptAnalyzer failures) (opens in a new window or tab).

[caption id="attachment_423" align="alignnone" width="750"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2017/01/one.png"><img class="wp-image-423 size-full" src="http://www.workingsysadmin.com/wp-content/uploads/2017/01/one-e1483731569927.png" width="750" height="504" /></a> Figure 1 Viewing the PSScriptAnalyzer results for a test script[/caption]

Here, you’ll see a more detailed summary of the results of the specific test. Click on Test Results to see more detailed results. You can scroll through the list and see specifically which tests failed.

[caption id="attachment_424" align="alignnone" width="411"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2017/01/two.png"><img class="size-full wp-image-424" src="http://www.workingsysadmin.com/wp-content/uploads/2017/01/two.png" alt="" width="411" height="151" /></a> Figure 2 Observing a specific failed test among passed tests[/caption]

Double clicking on a specific test that passed or failed will bring you to more detailed information, but what you probably actually want is the raw console output from the test. The raw console output is the only place you can see the line in your script or module that failed the test. What you see in the Stack Trace screen in the detailed view, is the line in the <strong>test</strong> that failed, not the line in the <strong>script that failed the test</strong>.

Close the tab that was opened to view detailed test results and you should return to the Test Summary screen. Click on “Download all logs as zip” button, and you can examine the raw console output.

[caption id="attachment_425" align="alignnone" width="584"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2017/01/three.png"><img class="wp-image-425 size-full" src="http://www.workingsysadmin.com/wp-content/uploads/2017/01/three-e1483731614879.png" width="584" height="154" /></a> Figure 3 Downloading the raw console output from a test[/caption]

In the .zip that you save, there is a Build folder. Open it and you will see .txt files containing the raw console output of the build, broken down by build step. Open the file for running the tests and you can see exactly what caused a specific test to fail.

[caption id="attachment_426" align="alignnone" width="950"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2017/01/four.png"><img class="size-full wp-image-426" src="http://www.workingsysadmin.com/wp-content/uploads/2017/01/four.png" alt="" width="950" height="303" /></a> Figure 4 Viewing the raw console output of a test and observing a PSScriptAnalyzer rule violation[/caption]

You can scroll through this output and see the same information for the other tests you ran. You may also wish to look through the other .txt files if you believe there may be errors in other parts of the build that could have generated raw console output.
