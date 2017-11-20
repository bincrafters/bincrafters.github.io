---
layout: post
title: 'Conan Package - MSYS2'
tags: [C++, Conan.io, Bintray]
comments: true
---

MSYS2 is software distribution and a building platform for Windows. It provides a Unix-like environment, a command-line interface and a software repository making it easier to install, use, build and port software on Windows. Many C++ projects are setup to be built with MSYS2 when built on Windows, rather than MSBuild. It is primarily intended to be used as a `build_requirement` in Conan recipes for these projects.  One project that requires MSYS2 to build from sources is Google's build system Bazel. 

## Package Reference

    msys2_installer/latest@bincrafters/stable
    
## Usage Information  

To get started with using the Bincrafters public Conan repository, please see this post:
[Bincrafters Conan Instructions](https://bincrafters.github.io/2017/06/06/using-bincrafters-conan-repository)

## Notes About this Package 

This excerpt is taken from [the `README.md` file of the github repository for this package](https://github.com/bincrafters/conan-msys2_installer).

MSYS2 never adopted semantic versioning, so this package offers a unique versioning option on the packages by using a "conan alias" named "latest".

[Conan Alias feature Explained](http://conanio.readthedocs.io/en/latest/reference/commands/alias.html?highlight=conan%20alias)

In summary, users can reference the version of "latest" in their requirements to get the latest release of MSYS2. "latest" is just an alias which redirects to an actual version of an MSYS2 package. MSYS2 rarely releases new versions, but when they do Bincrafters will compile, create and upload binaries for the package and "latest" will be updated to point to the new version. Because MSYS2 does not use semantic versioning, a datestamp will be used as the version number on the concrete Bincrafters packages for MSYS2 and the 'source()' method of each version of the recipe will use the latest tarball from the msys2.org repository here: 

[MSYS2 Distribution Repository](http://repo.msys2.org/distrib)

## Status - Stable
This package has been tested and is currently considered stable.  Please report any issues through the github repository for this recipe. 

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 
