---
layout: post
title: 'Public Trello Board - Need Contributors'
tags: [C++, Conan.io, Boost]
comments: true
---

We've added a [New Trello Board](https://trello.com/b/iFeFCPwa) to house all the packages that we discover we need to create some day to serve as dependencies, but that we don't really have time to build right now.  We hope that community members can work on these over time. 

For contributors who want to get involved, drop a note and feel free to take one of these on. Of course we'll be happy to help you along. 
 
---

## Current Packages
MPI is currently our biggest interest, as our it would really bring our Boost MPI package to a new level.  We would be able to have the default behavior be to install the appropriate MPI implementation for the operating system and then automatically pass that info to the Boost Package.  This would be a dramatic distinction and convenience when compared to installing and using MPI, Boost, and Boost.MPI through any other method (the status-quo being to set each up yourself, and then configure them to work together).  With Conan we can make it turn-key. 
