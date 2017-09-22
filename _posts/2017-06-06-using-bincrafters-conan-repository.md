---
layout: post
title: 'Using Bincrafters Public Conan Repository'
tags: [Conan.io, Bintray, C++]
---

Bincrafters is posting new packages and/or versions to our public Conan repository every week. We've provided some instructions below for users who wish to start using them. 

## Getting Started with Conan.io
If you're new to Conan.io, there's a great guide on how to get started here: 
https://conanio.readthedocs.io/en/latest/getting_started.html

The rest of this guide will assume you have a basic working knowledge of Conan.io, along with a working installation. 

## Adding the Bintray repository as a "Conan Remote"
By default, Conan will only search for packages from the two central repositories hosted and moderated by Conan.io staff: "conan-center" and "conan-transit".  Bincrafters packages are hosted in a separate Conan repository which is also hosted by Bintray, but which is managed by the Bincrafters team.  To start using any of the Bincrafters packages, simply run the command below:

	$ conan remote add bincrafters https://api.bintray.com/conan/bincrafters/public-conan

## Understanding Conan Channels
Conan has a somewhat unique but valuable notion of channels embedded in the package names.  An example package name is "Boost.System/1.64.0@bincrafters/stable".  The channel name in this example is "stable".  This is a required field for every package, but it's a completely arbitrary string meaning that authors can put whatever they want.  Bincrafters follows a somewhat standard convention popularized by the Conan teams own packages, which features two possible channel values:  `testing` or `stable`.   Under almost all circumstances, users should prefer the`stable` channel if it exists.  Packages in the `stable` channel are built automatically by Travis and Appveyor, which means they should have a wide variety of precompiled binaries corresponding to the most common build configurations.  In some cases, brand new packages may only feature a `testing` channel, but these packages would not be considered safe for general users anyway and are not supported.  

* Packager Tip: The CI process with Travis and Appveyor are made much easier thanks to a side-project from the Conan team called ["Conan Package Tools"](https://github.com/conan-io/conan-package-tools). Check it out if you've used CI before and plan to build packages. 

## Feedback
If you have questions about the Bincrafters repository, please feel free to email us: bincrafters at g mail dot com

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers.md). 