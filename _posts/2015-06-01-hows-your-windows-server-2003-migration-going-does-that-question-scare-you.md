---
layout: post
title: How's your Windows Server 2003 migration going? Does that question scare you?
date: 2015-06-01 12:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, end of life, microsoft, migration, mvp, windows server, windows server 2003, windows server 2012 r2]
---
Remember 2003? 2003 was a good year. Camera phones got popular, XBox took off, and I was a 14 year old in 9th grade. 2003 was also, obviously, the year that Microsoft released Windows Server 2003. Are you still running it? You shouldn't be, but I bet lots of you are. That should scare you because in less than six weeks from the time of this post, on July 14, 2015, Microsoft is ending support for Windows Server 2003. If you're not done your Windows Server 2003 migration to newer operating systems (Windows Server 2012 R2 is an excellent choice), or worse - not even started, you could face some very serious consequences. Let's answer a few questions you might have about that.

<h3>What does it mean to be unsupported?</h3>

In case "end of support" isn't clear, here's some of the highlights from the long list of concerns outlined in <a href="http://download.microsoft.com/download/D/8/D/D8D30224-9CE4-444F-AC06-7BAFCEADBC59/Windows_Server_2003_Why_You_Should_Get_Current_IDC_Whitepaper.pdf" target="_blank">this IDC white paper on why you should upgrade (pdf)</a>. There's tons of reasons but these were the ones that resonated with me.

<ul>
    <li>Elimination of security fixes.</li>
</ul>

Holy smokes. No more patches? For a second that almost sounds like a good thing, right? You're probably tired of patching servers. But, think of the consequences and implications of that. No more patches is a terrible, scary, awful thing. If I need to tell you why, you may consider a different career than the one that brought you to my blog. If you ever want to pass another audit, you better be receiving and applying security fixes for all your products, especially ones as fundamental as your Windows OSes.

<ul>
    <li>Lack of support.</li>
</ul>

Do you ever call Premier Support? Read Technet blogs or forums? Microsoft is shutting down support for Windows Server 2003 once it hits end of life. If you want help upgrading, you better get it now because after the end of life date, it might be a challenge to get.

Saying "I can put this off, I'm just going to buy extended support!" is the wrong attitude to have. First, you could buy an Egyptian pyramid for the amount of money that extended support is going to cost. Second, all you're doing is delaying the inevitable. You have to do this. Do it now. It's going to hurt more to put it off and do it later.

<h3>Okay, so there are some good reasons to get off Windows Server 2003 <span style="text-decoration: underline;">BUT</span> are there any good reasons to get on Windows Server 2012 R2?</h3>

There's tons. Windows Server 2012 R2 came out Q4 2013 and is the result of decades of learning, improvement, technological landscape shifting, development and a bunch of other buzz-verbs that all mean that it's better. It's better. Windows Server 2012 R2 is better than Windows Server 2003. Here's just a few articles that support that statement.

<ul>
    <li><a href="http://www.techrepublic.com/blog/10-things/10-compelling-reasons-to-upgrade-to-windows-server-2012/" target="_blank">10 compelling reasons to upgrade to Windows Server 2012 by Deb Shinder on TechRepublic</a></li>
    <li><a href="http://www.infoworld.com/article/2606748/microsoft-windows/108930-10-excellent-new-features-in-Windows-Server-2012-R2.html" target="_blank">10 excellent new features in Windows Server 2012 R2 by Paul Ferril on InfoWorld</a></li>
    <li><a href="http://windowsitpro.com/windows-server-2012/new-features-windows-server-2012-r2" target="_blank">New Features in Windows Server 2012 R2 by John Savill on WindowsItPro</a></li>
</ul>

If you look at all, you'll find thousands more articles, slides, posts, tweets, talks and more on the benefits and features of Windows Server 2012 R2 over its predecessors.

<h3>Upgrading is so intimidating. I need help! Where can I get some?</h3>

Microsoft has your back on upgrading and migrating. There are lots of guides and articles on these topics but Microsoft has assembled, in my opinion, <a href="https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx" target="_blank">the best resource hub out there</a>. Did you click that link? It takes you to <a href="https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx" target="_blank">the page with all the resources</a>. Click one of <a href="https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx" target="_blank">these links to go to that page</a>. I can't overstate how important I think it is that you <a href="https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx" target="_blank">go to this page and read about the resources</a> to help you migrate away from Windows Server 2003. All the links in this paragraph go to the same page. This is the page: <a href="https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx" target="_blank">https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx</a> . It's in your very best interest to go there and check out what's there. Need the link one more time? <a href="https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx" target="_blank">Here</a>.

Does it feel like I'm using this subsection of this post to direct you to <a href="https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx" target="_blank">Microsoft's page with tons of resources you can use to make your migration possible, if not easy</a>? It's because I am. There's tons of other resources out there, too, and they are a simple search away.

<h3>I get it. I want to upgrade. I've been pushing my organization to upgrade but I can't seem to get permission. What can I do?</h3>

Surely I've convinced you of the many great reasons to migrate away from Windows Server 2003 to Windows Server 2012 R2. These arguments make sense for an IT Pro but maybe not for an executive, business people, or sometimes even to a developer. Here are a few of the common ways I see resistance and my suggestions to overcoming them. Of course, every organization's politics are different and you may need to figure it out yourself.

<ul>
    <li>We have App XYZ that only runs on Windows Server 2003. It's crucial to our business. There's no new version.</li>
</ul>

Respectfully, if this is the honest to goodness truth for your organization, you might be on the Blockbuster/Kodak path of sustainability. Read this Wikipedia article on <a href="http://en.wikipedia.org/wiki/Diffusion_of_innovations" target="_blank">the theory of Diffusion of Innovations</a>. Take special note of chart that describes the different stages: Innovators, Early Adopters, Early Majority, Late Majority, and Laggards. You don't have to adopt every new innovation that comes across your desk, but if your entire business is dependent on a technology or product that is about to reach end of life, you're in trouble. You're already in the laggard stage of the adoption process if you're still not off Windows Server 2003. Just don't fall off the chart completely - get migrating!

<strong>There comes a point where you're not upgrading to gain an advantage, but to catch up to competitors who have already surpassed you.</strong>

<ul>
    <li>App XYZ is crucial to our business. There's a new version but we can't afford the down time to upgrade.</li>
</ul>

This one is easier to work with than the last one. Attack this resistance from two sides. First, reiterate the importance of upgrading and all the bad things that will happen if you don't. Second, and most importantly, find business reasons that make migrating to Windows Server 2012 R2 or the new version of App XYZ desirable to your specific stakeholders. Often with executives and business groups, it's even more important to <strong><span style="text-decoration: underline;">PULL</span> </strong>them towards something new as it is to <strong><span style="text-decoration: underline;">PUSH</span> </strong>them away from something old.

To address the downtime concerns, put effort into making a plan that makes the downtime as short and painless as possible. Do a side-by-side migration. Do the cut over at 3 in the morning when your customers are all asleep. Find a way to make the downtime as tolerable as possible.

<ul>
    <li>We don't need new features. We accept the risk of running in an unsupported fashion. It's just not worth our time to migrate.</li>
</ul>

This is a naive attitude, in my opinion. If you can't find a creative way to improve <em>anything</em> within your organization with even one new feature in Windows Server 2012 R2, you're not looking. A willingness to accept the risk of running unsupported demonstrates a lack of complete understanding of the risk involved with doing so. What would your customers say if you told them that your systems don't receive security updates any more? If you get resistance like this, you need to find a reason to pull your stakeholders towards the newer technologies and make sure they're clear on the risks of maintaining status quo.

<h3>Alright, I'm ready to take this on! Now how about a summary of some kind?</h3>

Glad you asked. If you take anything out of this post, make it these few things.

<ol>
    <li>Being unsupported is bad. Really bad. You don't want to be unsupported for a lot of reasons including no more security patches.</li>
    <li>Windows Server 2012 R2 has a ton of new features that make it a great OS to migrate to.</li>
    <li>Microsoft has <a href="https://www.microsoft.com/en-ca/server-cloud/products/windows-server-2003/default.aspx" target="_blank">a lot of resources available</a> to help you upgrade.</li>
    <li>Getting stakeholder permission for an upgrade is as much about selling the benefits of moving to a new system as much as it is about the disadvantages of staying on the old one.</li>
</ol>

Good luck and happy migrating!
