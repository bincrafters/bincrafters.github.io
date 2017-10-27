---
layout: post
title: 'Conan Packages - Boost v1.65.1'
tags: [C++, Conan.io, Bintray]
---

A few weeks ago, we announced a set of [Modular Packages on Conan.io for the Boost C++ Libraries](/_posts/boost-modular-packages-conan).  The original set of packages included Boost v1.64.0 only, and we've been working ever since to finish packaging v1.65.1.  We are happy to announce that the v1.65.1 packages are now available in the [Bincrafters public repository](https://bintray.com/bincrafters/public-conan).  

## Package Reference (Example)

    Boost.Stacktrace/1.65.1@bincrafters/stable
    
## Usage Information  

To get started with using the Bincrafters public Conan repository, please see this post:
[Bincrafters Conan Instructions](/_posts/using-bincrafters-conan-repository)

The package names are all Proper_Case with underscores when a name has two words (eg. `Poly_Collection`).  If you want to double check the package reference name, you can search the [Bincrafters public repository](https://bintray.com/bincrafters/public-conan).

## Notes About this Package 
You can find general notes about the Boost packages in the [original blog post](/_posts/boost-modular-packages-conan).  However, below you can find notes regarding any differences between the previous version and the current version. 

### New Libraries

This package brings two new libraries:  "Poly Collection" and "Stacktrace"

### Package Options
There are some new options on some of the packages, so below is the complete and current list for 1.65.1: 

|Package      |Option Name		| Default Values   | Possible Value    
|--------------|--------------------|-------------------|------------------
|All				|shared					| False                | True/False         
|Python		|python				| "python"          | string/path to local python install 
|Iostreams	|use_zlib				| True                | True/False         
|Iostreams	|use_bzip2			| True                | True/False  
|Regex			|use_icu				| True                | True/False  
|Locale	(new)|use_icu				| True                | True/False  


In the upcoming version of Conan (0.28) a new feature has been added which solves a significant problem with the Boost packages.  Users can now specify options using a wildcard syntax.  For Boost, this is most useful when specifying the `shared` option.  Thus, users can now specify that all Boost libraries should be compiled statically with one option statement as follows: 

	$ conan install -o Boost.*:shared=True

Previously, users had to specify each Boost library separately which was very tedious: 

	$ conan install -o Boost.Asio:shared=True -o Boost.Regex:shared=True ...

### Backporting improvements and fixes to 1.64.0
There were several package level fixes that were made for 1.65.1 and then backported to 1.64.0.  Of course none of this changes binary compatibility or anything at the C++ level, these changes generally just add support for additional configuration options, or properly compiling on various additional platforms.  One of the big improvements was adding builds for MacOS back to our Travis CI process.  Just before the announcement of the v1.64.0 packages, travis experienced issues with their Mac build environment which lasted several days.  We removed the Mac builds for x86 Architecture due to nuances with ICU on Travis.  If you use ICU on a MacOS with x86 architecture, the packages will still work, you will just need to use the `--build missing` conan option when running install, and let the packages build from source.  Feel free to reach out to us on Slack channel `#conan` if you have any issues or questions with this. 


## Status - Stable
This package has been tested and is currently considered stable.  Please report any issues through the github repository for this recipe. 

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 