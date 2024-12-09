---
layout: post
title: Writing Your Own Custom VSCode Snippets
date: 2018-04-25 07:30
author: thmsrynr
comments: true
categories: [editors, editors, PowerShell, powershell, snippets, vscode, vscode, workflow, workflow]
---
If you've seen any of the recent talks from Microsoft employees and MVPs about PowerShell, it's hard to miss that Visual Studio Code (VS Code/VSCode) is the new hot place to be writing your PowerShell code. VSCode with the PowerShell extension is the current Microsoft-recommended coding environment, whereas it used to be PowerShell ISE. ISE isn't dead (there are lots of posts on that), it's just considered to be complete, and all current development effort is focused on VSCode.

Great! Well, one of the things I like in my editor is my own custom snippets. I don't have very many, but I use the ones I have pretty often. Here's how to make one in VSCode.

<!--more-->

In VSCode, go CTRL + Shift + P to open the command pallet, and search for "Configure User Snippets". From there, you can do a new global snippets file, or choose the language that the snippets you're going to write are going to be for. This helps you separate your JavaScript snippets from your PowerShell snippets, and so on. I opened my powershell.json snippets file.

By default, the file includes a description, syntax and even an example of how to make a new snippet. I won't reproduce it here, but instead I'll share one of my most-used snippets and describe the different parts and how they work. They're declared in JSON.
```
"DateTime pre-pended Write-Verbose": {
    "prefix": "verb",
    "body": [
        "Write-Verbose \"[$(Get-Date -format G)] ${1:message}\"$0"
    ],
    "description": "Prepend datetime for Write-Verbose"
}
```
The name of my snippet is the first thing that's indicated, "DateTime pre-pended Write-Verbose", then the different properties that make up the snippet. The prefix I've given it is "verb", which you'll see the use for in a moment. Then, the body of the snippet. This one is just a "Write-Verbose" command, with part of the string to be written pre-populated. First, I'm writing the current time and date enclosed in square brackets, and then using the "${1:message}" notation, I'm placing the cursor at the location of that text, highlighting the word "message". This makes it so when you insert the snippet, the word "message" is already highlighted and you can just start typing your message. Then I have a "$0" at the end so when you hit tab, it takes you to the end of the line, outside the quotation marks of the "Write-Verbose". Finally, I gave the snippet a basic description.

To use the snippet, go CTRL + Shift + P to open the command pallet, find Insert Snippet, and type the prefix you gave your snippet - mine is "verb". Then once you hit enter, the body of your snippet will be inserted, and in my case, the word "message" is highlighted, right after the datetime.

That's all there is to it! If you want to see a bunch of awesome snippets written by the community, check out the <a href="https://github.com/PowerShell/vscode-powershell/blob/master/docs/community_snippets.md" target="_blank" rel="noopener">Community Snippets page</a> on the VSCode-PowerShell GitHub.
