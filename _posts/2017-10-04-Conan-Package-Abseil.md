---
layout: post
title: 'Conan Package - Abseil'
tags: [C++, Conan.io, Bintray]
---

Bincrafters has now published a Conan package for Google's open-source library "Abseil" to our public Conan repository on Bintray. Abseil was just announced by Titus Winters last week at CPPCon 2017, and provides a number of mature utililty types and functions.  Abseil is a bit unique in that Google has chosen not to implement semantic versioning and promote the use of the library strictly by following the master branch of their GIT repository, a strategy described by Winters as "Live at Head. 

## Package Reference

    abseil/latest@bincrafters/stable
    
## Usage Information  

To get started with using the Bincrafters public Conan repository, please see this post:
[Bincrafters Conan Instructions](https://bincrafters.github.io/2017/06/06/using-bincrafters-conan-repository)

## Notes About this Package 

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