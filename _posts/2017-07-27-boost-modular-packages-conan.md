---
layout: post
title: 'Boost - Modular Packages on Conan.io'
tags: [c++ conan bintray boost]
---

Starting with Boost 1.64.0, the Bincrafters team will now publish each of the Boost libraries as separate packages on Conan.io. With this, developers can now reference the specific Boost libraries they want to use as dependencies, rather than referecing the entire Boost collection. 

  ~~~
    [requires]
    Boost/1.64.0@conan/stable
  ~~~  

    ~~~
    [requires]
    Boost.Process/1.64.0@bincrafters/stable
  ~~~
 
---

## Technical Information
To get started with using the Bincrafters public Conan repository, please see this post: Bincrafters Conan Instructions

## Background Information
Please read on for more information about the project. 

### Boost Background
The Boost libraries have historically been released in the form of a single package which contains all of the libraries bundled together.  This provides a number of benefits, but also has significant and well-known disadvantages. For example, one of the oldest and most common requests from the Boost user community has been the ability to consume individual libraries from Boost without getting the entire bundle, something which has always been unsupported. While the Boost team is currently working toward changing this paradigm to something more modular, it will be some time until that effort is complete. Until then, Bincrafters will be publishing each release of the Boost libraries as modular pacakges on our public Conan repository.

### Conan.io Background
Conan.io provides a toolset and platform which is uniquely equipped to create and publish the Boost libraries as separate modular packages. The Bincrafters team felt this was a great opportunity, and decided to pursue it. Separating the Boost libraries into packages was difficult, however the flexibility and power of Conan made it not only possible, but also maintainable, which was a key concern at the start of the project. 






Conan.io provides the first dependency management platform of it's kind for C and C++. "Of it's kind" includes a number of characteristics such as being open-sourced, effective handling of the complicated challenge of native binary caching and hosting, and providing free hosting for OSS project packages and binaries powered by a leading cloud hosting provider for OSS packages: Bintray / JFrog. 


