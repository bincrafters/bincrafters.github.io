---
layout: post
title: 'Conan Package - Bazel'
tags: [C++, Conan.io]
---

Bincrafters has now published a Conan package for Google's open-source build system "Bazel" to our public Conan repository on Bintray. Bazel is used as the build system in a number of their popular C++ projects, including Abseil, Protobuf, Tensorflow, and others.  It is primarily intended to be used as a `build_requirement` in Conan recipes for these projects.  

## Package Reference

    bazel_installer/0.6.0@bincrafters/stable

    
## Usage Information  

To get started with using the Bincrafters public Conan repository, please see this post:
[Bincrafters Conan Instructions](https://bincrafters.github.io/2017/06/06/using-bincrafters-conan-repository)

## Notes About this Package 

This excerpt is taken from [the `README.md` file of the github repository for this package](https://github.com/bincrafters/conan-java_installer)

This Conan package contains the Java Development Kit (JDK). It is cross platform and is intended to be used as a Conan "build_requires" for C++ projects which require Java to be built. Google's build system "Bazel" is one particular example of a C++ build system which requires Java. Note that this package should not interfere or interact with other installations of Java on the machine. It does not change any persistent environment variables, it only adds/modifies those for the existing process. It passes the required environment variables to packages which require or build_require it through Conan's native env_info functionality.

This package is based on Azul Systems' Zulu build of OpenJDK. It's a certified and stable build that and functionally equivalent to Oracle's (as well as IBM's, Redhat's, and other certified builds). There are a number of advantages to using Zulu, which have caused many projects and organizations to use it as the default, including Microsoft Azure. If you are unfamilliar but interested in the differences between JDK providers, you are encouraged to research the topic.

## Status - Stable
These packages have been tested and are currently considered stable.  Please report any issues through the github repository for this recipe. 

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 