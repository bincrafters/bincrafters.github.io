---
layout: post
title: 'Boost 1.64.0 - Modular Packages on Conan.io'
tags: [C++, Conan.io, Bintray, Boost]
---

Starting with Boost 1.64.0, the Bincrafters team will now publish each of the Boost libraries as separate packages on Conan.io. With this, developers can now reference the specific Boost libraries they want to use as dependencies, rather than referecing the entire Boost collection. 

## Before
```
[requires]
Boost/1.64.0@conan/stable
```

## After
```
[requires]
Boost.Process/1.64.0@bincrafters/stable
```
 
---

## Technical Information
To get started with using the Bincrafters public Conan repository, please see this post: [Bincrafters Conan Instructions](https://bincrafters.github.io/2017/06/06/using-bincrafters-conan-repository)

## Package Options
Conan allows users to pass options to for each package upon install. The list of options for Boost packages are: 

|Package        |Option Name		| Default Values   | Possible Value    
|---------------|---------------------|-------------------|------------------
|All				|shared					| True                | True/False         
|Python			|python					| "python"          | string/path to local python install 
|IOstreams		|use_zlib				| True                | True/False         
|IOstreams		|use_bzip2				| True                | True/False  
|Regex			|use_icu					| True                | True/False  

*Note: The default option for "python" will search environment variables for a python install, and should find it by default on most systems*

## Conan Download and Cache Explained
If the Bincrafters repository contains a precompiled binary that matches your OS, compiler, and compiler settings, Conan will just download it to your local conan cache, and use it.  If it doesn't, Conan will download the recipe, build from source, and store the binary in your cache. Then, any future projects on that machine which use the same library (and the same compiler settings), will just use the binary in the cache.  This caching and re-use of compiled libraries is a cornerstone of Conan's efficiency benefits. 

## Continuous Integration
Bincrafters uses Appveyor and Travis CI to provide CI for all our packages.  This populates our Conan repository with not only the package recipes (which contain the build instructions), but also a wide array of pre-compiled Binaries for the most common operating systems, compilers, and settings.  The Conan team maintains a project called ["Conan Package Tools"](https://github.com/conan-io/conan-package-tools), which streamlines the CI process for us, making it much easier to maintain. 

## Background Information
### Boost Background
The Boost libraries have historically been released in the form of a single package which contains all of the libraries bundled together.  This provides a number of benefits, but also has significant and well-known disadvantages. For example, one of the oldest and most common requests from the Boost user community has been the ability to consume individual libraries from Boost without getting the entire bundle, something which has always been unsupported. While the Boost team is currently working toward changing this paradigm to something more modular, it will be some time until that effort is complete. Until then, Bincrafters will be publishing each release of the Boost libraries as modular pacakges on our public Conan repository.

### Conan.io Background
Conan.io provides a toolset and platform which is uniquely equipped to create and publish the Boost libraries as separate modular packages. The Bincrafters team felt this was a great opportunity, and decided to pursue it. Separating the Boost libraries into packages was difficult, however the flexibility and power of Conan made it not only possible, but also maintainable, which was a key concern at the start of the project.

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers.md). 