---
layout: post
title: Using PowerShell To List All The Fonts In A Word Document
date: 2016-10-05 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, automation, com objects, com objects, ms word, ms word, PowerShell, powershell]
---
Recently I was challenged by a coworker to use PowerShell to list all the fonts in a Word document. It turned out to be easier than I thought it would be... but also slower than I thought it would be. Here's what I came up with.

```
$Word = New-Object -ComObject Word.Application
$OpenDoc = $Word.Documents.open('c:\temp\test.docx')
$OpenDoc.words | % { $_ | select -ExpandProperty font } | select Name -Unique
$OpenDoc.close()
$Word.quit()
```

There could very well be a better way of doing this but this is what I came up with in a hurry. Line 1 declares a new instance of Word and line 2 opens the document we're looking at. Then, for each word (which is handily a property of the open word document), we're expanding the font property and selecting all the unique names of the fonts on line 3. Lines 4 and 5 close the document and quit Word.

So you can get something like this!

<a href="http://www.workingsysadmin.com/wp-content/uploads/2016/06/2016-06-24-10_31_12-Calculator.png"><img class="alignnone size-full wp-image-372" src="http://www.workingsysadmin.com/wp-content/uploads/2016/06/2016-06-24-10_31_12-Calculator.png" alt="Get All The Fonts In A Word Document Via PowerShell" width="673" height="257" /></a>
