---
layout: post
title: 'OSS vs Enterprise Dependency Management'
tags: [Conan.io, C++]
---

The domain of dependency management for C and C++ can be divided into to the smaller domains: OSS and Enterprise. Newcomers to Conan seem to be aware of the OSS domain, but often are completely unfamiliar with the enterprise.  This is a problem, because many of Conan's most powerful and important features are the ones designed specifically for the enterprise, so often time these users feel a bit lost about things they see in the documentation.  This post aims to help those newcomers understand the purpose and power of some of these enterprise-related features and shine some light on this lesser-known dimension of dependency management.

---

### Enterprise C and C++ Ecosystem Overview

While enterprise development environments are almost always private and proprietary, they still form an ecosystem.  Recently at the SwampUP devops conference there were a few dozen C and C++ developers and/or build engineers, almost all of them representing enterprise organizations and openly discussing their challenges around dependency management.  Perhaps unsurprisingly, there are a lot of shared challenges.  One thing that was certainly shared was that they had all done some research and/or testing with Conan and saw potential value for their build environment.  The situation is actually similar in the #conan channel in the cpplang.slack.com slack workspace.  There are a number of users who represent enterprise development teams with very large-scale challenges and are looking toward Conan as a solution.  They're not as vocal as the OSS enthusiasts, but they're generally easy to spot because they ask very different types of questions.  We're also starting to see less beginner questions about the basics Conan, and more advanced questions surrounding migrations to Conan from legacy solutions, which is interesting and encouraging. 

Certainly one of the most attractive things about Conan for these very large organizations is that it represents a single platform which is capable of wrapping around their most complex and obscure build scenarios for both their internal enterprise code as well as whatever OSS libraries they use.  While there are a number of other novel package managers popping up in the C++ ecosystem, they're almost exclusively focused on trying to make the OSS library ecosystem simpler.   None are designed to address these highly complex enterprise build environments.  This effectively means that Conan the only platform of it's kind, and since many of them already use JFrog's Artifactory service for managing other package types, adding Conan repositories on their existing servers, making it overwhelmingly attractive as a solution. 

So now that we've talked a bit about the landscape of enterprise package management, lets talk about a few of the Conan features which actually solve problems and deliver value in these environments. 

### Source, Binary, System, and Tools

Package management (or the more general term "dependency management") is the well-known marquee feature of Conan, and thus not intended to be the focus of this article.  However, it's important to clarify some points about how Conan dependency management differs from others.  Conan provides four parallel components surrounding the packaging and management of dependencies for projects.  While enabling users to package source files (as do other package managers), Conan also enables users to package compiled binaries, and the build tools used to compile the sources into binaries.  It also lets users specify dependencies from other package managers, namely those built into the common operating systems.  In particular, the management of binaries and build tools is one unique and powerful feature which is used extensively in the enterprise use-case, and relatively rarely in the OSS use-case (although that is changing slowly).  By providing all of these slightly different "dependency management" features through a unified interface, platform, and syntax, it really simplifies the shape of the problem from an administrative point of view.   

*Note: For more detail about binary and tool packaging, check out our upcoming blog post titled "What is Conan?".* 

### Profiles

Of all the under-appreciated features in Conan, profiles have to be the single most powerful and transformative.  At SwampUP, virtually every presentation came from developers who use Conan in an enterprise codebase, and virtually all of them talked about their use of profiles.  So what makes profiles so important?  

In order to make a powerful and valuable transformation across many organizations in an industry, there has to be something really wrong.  Something broken or horribly inefficient, and so complicated that it hasn't been fixed in a simple and general way.  Right?  One would think so, but Conan profiles actually seem to defy this logic.  What Conan profiles actually do is actually straightforward (although the road of creating and evolving the functionality was not).  As it stands now, Conan Profiles could potentially stand alone as a tool which would be generally useful across all of software development.  Here's what Conan profiles offer: 

- Robust Environment Variable Management
- Build tool installations, decoupled from the OSS
- Build toolchain file management
- Robust compiler and cross-compilation control
- A composition and distribution strategy for the above
- It's open-source, tested, and mature (unlike in-house tools)

*Note: For more detail about profiles, check out our upcoming blog post titled "What is Conan?".*

With the ability to compose and distribute the profile system among enterprise teams, Conan profiles have truly revolutionized a growing number of enterprise workflows and strategies in a way that would not be possible without them.  It has proven to be an absolutely necessary abstraction layer to corrale all the inputs to build processes.  

Ref. Conan Profiles: 
[https://docs.conan.io/en/latest/reference/commands/misc/profile.html](https://docs.conan.io/en/latest/reference/commands/misc/profile.html)

### Customizable Settings - Compilers and Architectures

How many compilers are there for C and C++ ?  Most developers are probably aware of at least 3 or 4,  and might think that 10 is a generous guess.  The most honest answer is probably that nobody knows.  50 probably sounds like a reasonable guess, but it the real number is certainly far greater than that.  Thus, Conan takes the approach of supporting an infinite number of compilers, by defining a few well-known compilers for practicality and convenience, but giving developers the ability to define whatever compilers are used their environment, and their properties.  One crucial property that Conan empowers users to define and control is the "ABI compatibility" properties of a compiler.  For example, binaries built from different GCC minor versions are ABI compatible, but only those after 4.9.  Similar situations exist with obscure enterprise compilers.  Conan is designed to handle these situations with ease.  Similar to the problem of knowing all compilers, it's impractical and useless to try to know or define all possible architectures. Thus, again the best solution for a tool like Conan is to provide sensible defaults but empower developers to define the ones they care about (which it does).  

Conan users who want to use exclusively for getting dependencies for OSS projects rarely use obscure compilers and architectures, so this is a great example of a feature which is predominantly designed for enterprise projects and seems unnecessarily complicated to the newcomer.  With that said, the IOT revolution and explosion of custom architectures is making this a more relevant feature for people who do development for new and obscure hardware platforms as a hobby. 


### Custom Generators for Build System Variables

Have you ever heard of OpusMake?  
[http://www.opussoftware.com/](http://www.opussoftware.com/)

I hadn't heard of it, but I was tasked with automating builds with it. Unfortunately, CMake was not usable in the codebase, so I needed a way to generate make files manually.  Also, the syntax of OpusMake is proprietary, very different from GnuMake, so even if there was an existing way to generate Makefiles, it wasn't going to help me.  Fortunately, it was trivial in Conan to write a custom Generator that passed the information to OpusMake in its native format and use it throughout our environment.  

This is a common situation in many enterprise organizations.  Their requirements might include building projects with in-house, vendor provided, or just really old build systems, none of which would ever be natively supportable by any package manager (including Conan). So, similar to the virtues mentioned above (the features around profiles and settings), the crucial requirement around build systems is flexibility and Conan provides a really powerful model for that. 

Ref. Conan Generators: 
[https://docs.conan.io/en/latest/reference/generators.html](https://docs.conan.io/en/latest/reference/generators.html)

### Summary

Hopefully you will come away from the post with a better understanding of why the Conan documentation makes it appears a little more complicated than NPM, Maven, and perhaps most of the other package managers for C and C++.  And, if you work in a large scale enterprise codebase, we hope we've highlighted some feaures that are relevant to your current challenges.  In any case, we think it's important to help those who are actively exploring Conan to see it clearly for all that it does, and hopefully learn a few things along the way. 
