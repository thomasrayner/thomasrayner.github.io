---
layout: post
title: Custom PSScriptAnalyzerRule - Function Capitalization
date: 2017-05-24 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, DevOps, devops, Pester, pester, PowerShell, powershell, pssa, PSScriptAnalyzer, psscriptanalyzer, regex, regex]
---
I've got a number of custom PSScriptAnalyzer rules that I sometimes run. A little while ago I <a href="https://github.com/ThmsRynr/CustomPSSARules/" target="_blank">uploaded them to GitHub</a> to share with others. Today I'm going to walk you through the <a href="https://github.com/ThmsRynr/CustomPSSARules/blob/master/Casing/Rules/AvoidImproperlyCapitalizedFunctionNames.psm1" target="_blank">AvoidImproperlyCapitalizedFunctionNames rule I wrote</a>.

<!--more-->

I wrote documentation (and tests) for these with the intention of someday making a pull request to PSSA to add these rules, but <a href="https://github.com/PowerShell/PSScriptAnalyzer/issues/743" target="_blank">PSSA is not currently set up to include script-based rules</a>. Here's the description of my rule, from the documentation I wrote.

<blockquote>According to the PowerShell Practice and Style guide's section on <a href="https://github.com/PoshCode/PowerShellPracticeAndStyle/blob/master/Style%20Guide/Code%20Layout%20and%20Formatting.md#capitalization-conventions">capitalization conventions</a> (community developed, but referencse Microsoft's <a href="https://msdn.microsoft.com/en-us/library/ms229043?f=255&amp;MSPPError=-2147217396">published document</a> on the same for the .NET framework), it is best practice to use PascalCase for functions inside of modules and scripts. This means that that one should never see adjacent capital letters in a Function name.

An exception exists for two letter acronyms only like "VM" for Virtual Machine or "PS" for PowerShell (ex: <code>Get-PSDrive</code>). This should not extend to compound acronyms like Azure Resource manager's "RM" meets Virtual Machine "VM" in <code>Start-AzureRmVM</code>. Accordingly, this rule warns on instances where four or more adjacent capital letters are found in a function name.</blockquote>

With this description, it's no surprise that my rule will identify functions with 4 or more adjacent capital letters. It's not a perfect solution, because people could still implement things in all lowercase, or with other improperly capitalized names, but it's a good start.

```
function Test-FunctionCasing {
    [CmdletBinding()]
    [OutputType([PSCustomObject[]])]
    param (
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [System.Management.Automation.Language.ScriptBlockAst]$ScriptBlockAst
    )

    process {
        try {
            $functions = $ScriptBlockAst.FindAll( { $args[0] -is [System.Management.Automation.Language.FunctionDefinitionAst] -and  
                $args[0].Name -cmatch '[A-Z]{4,}' }, $true )
            foreach ( $function in $functions )
            {
                [PSCustomObject]@{
                    Message  = 'Avoid function names with more than 3 capital letters in a row in their name'
                    Extent   = $function.Extent
                    RuleName = 'PSAvoidImproperlyCapitalizedFunctionNames'
                    Severity = 'Warning'
                }
            }
        }
        catch {
            $PSCmdlet.ThrowTerminatingError( $_ )
        }
    }
}\n```

Custom PSSA rules need to take some sort of AST object, and mine takes a ScriptBlockAST so it can go through all the declared functions in that AST. Line 12 will get all the function definitions with names that have 4 or more adjacent capital letters. For each of those, I return a PSSA warning about violating the naming convention.
