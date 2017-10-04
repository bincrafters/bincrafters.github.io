---
layout: post
title: 'Conan Package - Abseil'
tags: [C++, Conan.io, Bintray]
---

Bincrafters has now published a Conan package for Google's open-source library "Abseil" to our public Conan repository on Bintray. Abseil was just announced by Titus Winters last week at CPPCon 2017, and provides a number of mature utililty types and functions.  Abseil is a bit unique in that Google has chosen not to implement semantic versioning and promote the use of the library strictly by following the master branch of their GIT repository, a strategy described by Winters as "Live at Head."

If you've been following bincrafters the past few days, you've seen our recent releases of a Java package, followed by Bazel.  Some may have wondered why anyone would create and publish these packages as their purpose in Conan was not obvious.  The reason was Abseil.  Since the announcement of Abseil, we wanted to try it out and help others try it out more easily via Conan.  However, you can't just package Abseil, you have to build it first which is non-trivial.  Still, we decided it was worth the effort to do it right and and actually use the build system supported by Google, and create the actual dependency chain in Conan.  There are some efforts that aim to build Bazel with CMake, and that's probably a good thing.  However, we felt that when it comes to building and packaging Google libraries in a repeatable and supportable way, it was best to embrace Bazel in our packaging pipeline.  In fact, we discovered some pretty impressive things with Bazel, so it was for the best.  Also, with Google releasing other great OSS libraries like Tensorflow and Protobuf to name a few, we now have the tools to release packages for these projects much more easily.  So, stay tuned if you're interested in these projects, and please let us know what libraries you want via twitter or trello (see sidebar). 

A final note, Abseil was announced just about a week ago, and so it's a testament to the power of Conan.io that we have been able to create and test these three packages in a weeks time. It really is a brilliant platform. 

## Package Reference

    Abseil/latest@bincrafters/stable
    
## Usage Information  

To get started with using the Bincrafters public Conan repository, please see this post:
[Bincrafters Conan Instructions](https://bincrafters.github.io/2017/06/06/using-bincrafters-conan-repository)

## Notes About this Package 

Even if you are not new to Conan, there are some nuances to the Abseil package users may need to know.  Please read on for more details. 

This excerpt is taken from [the `README.md` file of the github repository for this package](https://github.com/bincrafters/conan-abseil).

Abseil has a unique versioning philosophy, so this package offers a unique versioning option on the packages by using a "conan alias" named "latest". 

["Conan Alias feature Explained"](http://conanio.readthedocs.io/en/latest/reference/commands/alias.html?highlight=conan%20alias)

In summary, if users want to follow the Abseil philosophy of "Live At Head" as closely as possible while getting the benefits of using Conan, they can reference the version of "latest" in their requirements as shown in the example below.  "latest" is just an alias which redirects to an actual version of an Abseil package. Bincrafters will compile, create and upload binaries for the package on some recurring basis, and "latest" will regularly be updated to point to the most recent one.  Of note, because Abseil does not use semantic versioning, a datestamp will be used as the version number on the concrete Bincrafters packages and the `source()` method of each version of the recipe will point to the most recent commit of Abseil available at the time that package version was created.  Currently, there is only a "master" branch for Abseil. 

The result of using "latest" is that whenever Bincrafters uploads a new version of the recipe and updates the alias, your next call to "conan install" will download (or build if necessary), and the immediately begin using the latest version of Abseil. 

If users want to use Abseil, perhaps staying up to date but with slightly more control over when the updates happen, they can choose to point to the concrete packages. Pointing to concrete packages by date has many other uses, such as going back to a specific point in time for troubleshooting. 

## Status - Stable
This package has been tested and is currently considered stable.  Please report any issues through the github repository for this recipe. 

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 