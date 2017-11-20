---
layout: post
title: 'Conan Package - Bazel'
tags: [C++, Conan.io, Bintray]
comments: true
---

Bincrafters has now published a Conan package for Google's open-source build system "Bazel" to our public Conan repository on Bintray. Bazel is used as the build system in a number of Google's popular C++ projects, including Abseil, Protobuf, Tensorflow, and others.  It is primarily intended to be used as a `build_requirement` in Conan recipes for these projects.  

## Package Reference

    bazel_installer/0.6.0@bincrafters/stable
    
## Usage Information  

To get started with using the Bincrafters public Conan repository, please see this post:
[Bincrafters Conan Instructions](https://bincrafters.github.io/2017/06/06/using-bincrafters-conan-repository)

## Notes About this Package 

This excerpt is taken from [the `README.md` file of the github repository for this package](https://github.com/bincrafters/conan-bazel_installer).

Bazel is an open-source build system released by Google which is written in Java, and effectively required to build all of their open-source C++ libraries. While many C++ developers may want to utilize Google's C++ libraries, Bazel presents some challenges. For example, most C++ developers outside of Google have never used Bazel. Also, many C++ developers may not have a suitable Java version installed. Thus, the overall proposition of Bazel is regarded as unreasonable by some, and in many cases passed over by those who were initially interested. The "overall proposition of bazel" being the requirement of installing Java which is disagreeable to some, in order to install Bazel which they'll have to learn from scratch just to utilize a few Google projects.

This Conan.io package aims to make it trivial for C++ developers to incorporate Googles C++ libraries in their projects, by removing the need for the developer to deal with anything related to Bazel.

This package contains pre-built binaries of Bazel for Windows, Mac, and Linux, and includes an option to include an embedded JDK if the local machine does have a suitable version already. It intended to serve as a building block for future packages which will contain Google's open-source C++ libraries. These future Conan packages will reference this package as a build_requirement. This means that whenever one of these other Google libraries needs to be compiled, Bazel will be automatically downloaded and used to perform the build. This download will only occur once for the machine however, as Bazel will be cached in the local Conan cache for reuse.

## Status - Stable
This package has been tested and is currently considered stable.  Please report any issues through the github repository for this recipe. 

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 
