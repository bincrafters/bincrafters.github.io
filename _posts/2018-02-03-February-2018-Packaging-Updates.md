---
layout: post
title: 'February 2018 Packaging Updates
tags: [Conan.io, Bintray, C++]
---

January 2018 proved to be one of the busiest and most challenging months ever for Bincrafters.  As stated previously, we've been toiling away at upping our quality game and working through the results of the "great pakage refresh" we started in December.  We've now weathered the storm, and looking forward to making a number of great announcements in the weeks to come. Here's a few right now. 

## Strategic Movement on Conan Center  
If you follow @conan_io or @bincrafters on twitter, you have probably started to see some new package announcements for Conan-Center.  If not, we encourage you to take a trip over there and browse the current listing.  In any case, what we really want to point out is the bigger picture of what's taking place with regard to prioritization of packages.  Broadly speaking, Bincrafters have begun by submitting a number of packages in the following categories: 

* Unit Testing
* Logging
* Compression
* Parsing and Formatting
* Build Requirements

These might not seem terribly exciting to Conan users because in many cases they are header-only, or are relatively easy to build, and don't do anything flashy.  However, the world of packaging is a world of layers, and these represent the low-level "foundational" on which countless libraries are built. So, we simply had to start with these and make sure they were mature and stable before moving on to the "really cool stuff."  As the Conan team has already helped us work through this first group, we've started on the next group.  So, in the coming weeks, you should also start to see packages from the following categories hit Conan Center: 

* Image Formats
* Audio Codecs
* Encryption Libraries
* Async/Event Libraries

Again, these libraries can be described as "foundational", but perhaps just a slightly higher layer than logging and testing.  These libraries also have the distinction of being used by multiple members of the Bincrafters team on their own projects.  As stated on the Bincrafters blog, we put significant priority on the packages our contributors need to use, because meeting our own packaging needs is what brought us together around Conan in the first place.  

## An Update on Frameworks and Super-Libraries  
Boost, Qt, wxWidgets, FFMpeg, Xiph, OpenCV, Folly, EASTL, XFML, CGAL... etc. 

These are the projects that we know users really struggle with building and maintaining.  Now that our CI is really streamlined, flexible, and maintainable, we actually start to approach these projects with maximum efficiency and a sense of confidence. Also, crucially, there have been significant improvements and patches that will dramatically streamline some of these recipes, as well as some currently in development.  This includes some optimizations around various compiler flags, and some new features around toolchains.  

## Normal Modern Libraries
Again, with the recent improvements in our standards and templates, we can now actually get back to the vast number of "regular libraries" on the backlog (as well as those stalled in the current pipeline).  This will result in much more visible strides, including mature packages for libraries like ZeroMQ, SqLite, CPPRestSDK, and countless others.  The goal is to have a steady stream of these flow from our team to Conan Center throughout the next year.  In the past, many of these were waiting on some of the "foundational" dependencies mentioned before, or raised some number of questions about maintainability or technicalities.  For example, how to handle of Makefile-only libraries on Windows, how to handle libraries which need `pthread` on linux or `ws2_32` on Windows, how to manage environment variable propogation, whether or not to include MinGW in our CI:  these topics were all under discussion over the past 5 months.  During that time, we were learning so much that the templates were changing almost daily. The good news is that now, we've chosen strategies for most of these and that really frees us up to get more things done without having philosophical quandries about every new package. We'll continue to evolve, but not as rapidly as before. 

## Getting Back to the Main Mission 
After so much groundwork and the stability promise of Conan 1.0, we feel we can FINALLY start getting into the fun part of the mission which we should all remember:  enabling a modern package-based developer experience like we have in other languages.  This means packaging many more "single-purpose" "best-in-breed" libraries as opposed to super-libraries, and offering modern library authors a clear and mature strategy for adding `conanfile.py` to their project and maintaining it long-term.  The doors are now open for substantially more progress than Conan.io saw last year, and so we encourage you to stay tuned to @conan_io and @bincrafters on twitter for the rest of 2018.  


