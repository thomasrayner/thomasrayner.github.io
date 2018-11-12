---
layout: post
title: Referencing Non-String Hashtable Keys in PowerShell
date: 2017-11-15 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, PowerShell, powershell]
---
Say you've got a hashtable with a bunch of data in it, but the key is not a string. How do you refer to specific items?

You can set something up to experiment with this with this code.

<!--more-->

```
PS&gt; $a = @{}
PS&gt; 1..3 | % { $a.add($(New-Guid), $_) }
```

Declare $a as a new empty hashtable, and then add three items to it. The key is a GUID, and the value is just a number. You get something like this.

```
PS&gt; $a

Name                           Value
----                           -----
a2022422-ffe6-4291-a736-c1d... 1
33b8251c-8c09-433c-ae88-666... 3
4d9d41c1-8a0b-4326-ad59-164... 2
```

Now say you want to refer to the first item in the list whose key/GUID is a2022422-ffe6-4291-a736-c1de97720f25, in my example. You could try any of these.

```
PS&gt; $a.a2022422-ffe6-4291-a736-c1de97720f25
PS&gt; $a.'a2022422-ffe6-4291-a736-c1de97720f25'
PS&gt; $a['a2022422-ffe6-4291-a736-c1de97720f25']
PS&gt; $a.Item('a2022422-ffe6-4291-a736-c1de97720f25')
```

But none of these actually return any information. The problem is that the key is a GUID, not a string, but we're trying to refer to it as a string. Instead, you have to treat it like a GUID.

```
PS&gt; $a[[guid]'a2022422-ffe6-4291-a736-c1de97720f25']

1
```

By casting the string as a GUID, you're telling the hashtable that you're not just looking for a string. This same thing works for other data types like integers.
