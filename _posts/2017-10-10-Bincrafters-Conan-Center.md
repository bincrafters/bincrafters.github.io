---
layout: post
title: 'Bincrafters Packages and Conan Center'
tags: [C++, Conan.io, Bintray]
---

"Conan Center" is the moderated central repository for Conan packages hosted by Bintray.  With Conan Center, community members need only to check a box on their package in the web portal and it will be submitted for moderation and inclusion.  This strategy is very elegant, and actually has been used to great success for several years with their moderated central maven respository for Java packages known as "JCenter".  

The advent of Conan Center is possibly the most important step forward for Conan as a central package repository for open-source C++ packages.  The long-term goal for most of the packages in the Bincrafters public repository will be to submit the packages for inclusion into Conan Center, until such time as each library author expressess the desire to maintain their own package in Conan Center (for example, Eric Neibler and Ranges V3).  We have reached out to several popular library authors and offered to assist in helping the get started with packaging their library with Conan, and are currently working with some to that end. For the others, we will continue to create and maintain packages for requested open-source libraries in our public repository, and submit them to Conan Center when ready. The more people that use our repository and provide feedback, the more mature and robust those packages will be when they are submitted.  

** Motivations 

Thus the [Public Bincrafters Repository](https://bintray.com/bincrafters/public-conan) is intended to solve a few problems for ourselves and the community.  

The first was somewhat personal, most of us wanted to collaborate and work as a group rather than solo.  It's somewhat thankless work, but when you're working in a team it feels more like a community contribution and it's more motivating.  Also, there is a great deal of knowledge and skill that goes into cross-compiling the vast sea of open-source C++ libraries, and the sharing and learning among the team has been remarkable.  Each member has come with a unique background and specialty, and has contributed important knowledge to the team. 

The second reason is perhaps more fundamental and practical.  To build larger libraries with dependencies, we first had to build a foundation of reliable packages containing those dependencies (libraries for parsing, encryption, compression, etc).  The strategy of depending on packages that existed in other remotes outside of Conan Center and Bincrafters was simply not maintainable.  For ourselves and the community to use our packages, it was clear that all of our dependencies needed to exist in one of these two repositories.  It was also clear that this problem was not unique to C++ or Conan.  In many ways the situation is very similar to that of RPM fusion for Feodra/Centos/Redhat linux.  The existance of repositories with large numbers of curated packages run by a team in the community can provide a great deal of benefit, even with a strong healthy moderated central repository. 

** Summary
Over time, Conan Center will feature many great packages for C and C++ libraries, enabling users to leverage dependencies exclusively from that one repository. The Bincrafters repository aims to support that initiative by contributing as many packages to it as we can, and by using our packages and providing feedback, developers can play a vital role in the success of this effort. 