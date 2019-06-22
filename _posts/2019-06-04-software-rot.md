---
layout: post
title:  "Technical rot: the missing metaphor"
author: steve
categories: [ Engineering, Management ]
image: assets/images/rot.jpg
featured: true
permalink: /blog/:title
---

On the face of it, the term 'technical rot' does not seem to make much sense. After all, computer code is not organic. It does not corrode. It does not break down.

Here's some code.


    a = 1
    b = 2
    c = a + b
    print c

You can sleep safe in the knowledge that this code will still run perfectly thirty years from now. 

Unfortunately, most production code doesn’t look like the example above. It looks like this:

    import thirdpartyhairball
    a = 1
    b = 2
    c = thirdpartyhairball.add(a, b)
    thirdpartyhairball.save(c)

Developers incorporate a huge amount of "other people's code", primarily open source code, into their codebase, as dependencies, in order to maximise their productivity.

Like a tent perched on top of a mountain, the code written for a product itself is now often merely a tiny layer of glue code on top of a vast body of other people's code; libraries, database engines, operating systems and frameworks. A single dependency can drag in comically huge sub-hierarchies of dependencies, particularly in javascript. It is not uncommon for a modern front end to have over 1,000 node library dependencies.

The diagram below is roughly to scale and illustrates the number of lines of code powering the software stack for a typical startup that has been running for a few years. The black triangle perched on the top accounts for all the code authored by a team of five engineers working for two years: ~200,000 lines of javascript, python, html and css in the git repo, in relation to the volume of code in the dependencies below.

![Tent]({{ site.url }}/assets/loc_ratios.png)

Unseen legions of developers, working in different companies and on open source projects across the world, are continuously modifying this mountain of code to fix bugs, add new features and remove old features. Now, obviously a given library will only change occasionally, and often the changes are backwards compatible so upgrading is cheap, but with thousands of dependencies in play these dependencies need to be continuously monitored for vulnerabilities, patches and updates. This continuous environment drift over time is how entropy seeps into your code. This force acting on your software is called 'software rot' and continuous engineering effort, in the form of upgrading libraries, is required to counteract this force.

Leveraging third-party code as dependencies is not a luxury or a short-cut; it is a necessity. Most software projects built today would simply not be viable without leveraging libraries and frameworks. But just because these are free to use represent a great trade-off, that does not mean there is no further 'price' to pay. Dependencies need to be maintenanced and the effort to do so is proportional to their number, size and maturity. The more features you have the more dependencies you tend to introduce.

So why do we ignore software rot? Why do technology teams routinely fail to educate their stakeholders about this reality at the outset of projects, and the long term cost implications of tradeoff decisions they are making.

Well, the main reason  software rot is not a first class concept is that it is invisible at small scale in young codebases. When an application is initially being built the whole codebase is being touched, tweaked and modified continuously, and the work to upgrade dependencies is being silently smuggled inside new feature development stories.

Rot, true to the analogy, only surfaces after a few years. Rot often first manifests itself as bug discovered in large, stable area of an old code base that nobody has touched for years. The bug is traced to a library, and a fix is available in the latest version. Perhaps that version is is minor version upgrade that is backwards compatible with no breaking changes. These are quick to upgrade, necessitating only just a (hopefully automated) regression test run and push to production. Perhaps it requires the upgrade of another more significant dependency with breaking changes that necessitate reworking a large chunk of the codebase.

Getting blindsided like this is not fun. Explaining to stakeholders why you have to stop work for weeks to upgrade your codebase can, quite rightly, test relationships. It's at this point that many team will roll their eyes and explain that this is 'technical debt' introduced by some previous ne'er-do-well engineer. This is both a missed opportunity and another criminal abuse of the metaphor of 'techcnical debt', to add to litany of abuse of that metaphor.

Technical debt is a wonderfully apt metaphor coined by Ward Cunningham to capture a phenomenon seen when you build software. During the process of modelling a real world domain or process in code, we make mistakes, because we are human. Perhaps our model is imperfect because we discover some relationship that is not reflected in our code, or we fail to efficiently layout our code in a way that makes it easy to modify in the future. The debt is the work we should do to correct the model, but forgo temporarily. The interest payment on technical debt is paid when and if we try to change the code subsequently without first making the correction. If we don't need to modify the code again, we may not ever have to pay the debt.

Technical rot is fundamentally different to technical debt. Technical rot materialises over time in dependencies. Stretching the metaphors, the payments of technical debt are triggered by the act of needing to change the code. The payments of technical rot are triggered by the passage of time.

It's easier to illustrate the value of maintaining a distinction between these two concepts by considering scenarios when they interact with each other.

First, consider an early stage startup with a small, but rapidly evolving codebase. Although this team may choose, quite legitimately, to judiciously take on copious technical debt, just to get features out the door and get user feedback, the code will not sit unchanged long enough for technical rot to emerge as an issue at all.

Second, consider a small team that is babysitting a very large, well designed legacy platform that is now in maintenance mode, with no new features being added. This team will probably have very little technical debt to worry about because the product was so well designed, but they will inevitably have to spend a big proportion of their time keeping on top of technical rot, by upgrading libraries and working through breaking changes in a huge codebase.

Finally, consider the scenario where this same small team is maintaining a very large application with lots of dependencies and a poor design containing lots of technical debt. This team will have to cope with a large surface area of code rotting and, because of the technical debt, the cost of servicing that rot will be very high. Each time they want to make a change to fix some rot they are forced to work around the technical debt. To combine metaphors, each time they are forced to pay the tax that is the technical rot, they also have to pay interest on the technical debt. It is easy for teams can to paralysed by dilemmas of the form: do we spend 2 weeks to fix the the debt so we can fix the rot in a day, or do we just take a week fix the rot and work around the debt, leaving it unresolved? In some cases these twin headwinds of technical debt and technical rot can overwhelm teams entirely.

Technical rot is critical concept to be able explain to your business stakeholders because it profoundly affects the long term economics of large software platforms, and the economics of leaving unused experimental features in a product. I recommend adding it the trinity of 'features, 'bugs' and 'technical debt'.


------

To delete:


It is important not to dump all technical problems into a giant bucket labelled 'tech debt', and let technical debt become a pejorative term. Technical debt is often introduced accidentally. Other times you will want to agree with stakeholders to use it as a legitimate, sensible cost saving tactic. You might want to say to stakeholders "so lets agree we will take on some tech debt here to build this prototype faster because you might just throw it away". If software rot is lumped together with technical debt, which in turn is allowed to become an undifferentiated euphemism for 'shit software', you cannot bind your stakeholders to these kind of agreements, because they are essentially meaningless.



