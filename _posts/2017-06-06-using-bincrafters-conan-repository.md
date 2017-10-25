---
layout: post
title: 'Using Bincrafters Public Conan Repository'
tags: [Conan.io, Bintray, C++]
---

Bincrafters is posting new packages and/or versions to our public Conan repository every week. We've provided some instructions below for users who wish to start using them. 

## Getting Started with Conan.io
If you're new to Conan.io, please start with [Conan's Official Getting Started Documentation](https://conanio.readthedocs.io/en/latest/getting_started.html)

The rest of this guide will assume you have a basic working knowledge of Conan.io, along with a working installation. 

## Adding the Bincrafters repository as a "Conan Remote"
By default, Conan will only search for packages from the two central repositories hosted and moderated by Conan.io staff: "conan-center" and "conan-transit".  Bincrafters packages are hosted in a separate Conan repository which is also hosted by Bintray, but which is managed by the Bincrafters team.  To start using any of the Bincrafters packages, simply run the command below:

	$ conan remote add bincrafters https://api.bintray.com/conan/bincrafters/public-conan

## Understanding Conan Channels
Conan has a somewhat unique but valuable notion of channels embedded in the package names.  An example package name is:

	Boost.System/1.64.0@bincrafters/stable

The channel name in this example is "stable".  This is a required field for every package, but it's a completely arbitrary string meaning that authors can put whatever they want.  Bincrafters follows a somewhat standard convention utilized by the Conan teams own packages, which features two possible channel values:  `testing` or `stable`.   Under almost all circumstances, users should prefer the`stable` channel if it exists.  In some cases, brand new packages may only feature a `testing` channel, but these packages would not be considered safe for general users anyway and are not supported.  

## Packages without official releases
The notation shown below is used for publishing packages where the original library does not make official releases. Thus we use a datestamp to show when the package was created:

	gsl_microsoft/20171020@bincrafters/stable
	
## Packages without semantic versioning
The same notation is used for publishing packages where the original library does have official releases, but does not use semantic versioning. In this case, the version number is the one provided from the original library.  In the case of `msys2_installer`, the library happens to use a datestamp:

	msys2_installer/20161025@bincrafters/stable 
	
## Conan "latest" version convention
In some cases a version alias of "latest" is added to packages ([Conan Alias feature Explained](http://conanio.readthedocs.io/en/latest/reference/commands/alias.html?highlight=conan%20alias)
).  Users can reference this version in requirements as shown in the example below to get the latest release without specifying a specific version or range: 

	msys2_installer/latest@bincrafters/stable 
	
*Note that using the `latest` will cause your projects to download and use an updated version as soon as it becomes available.  Such library updates can potentially be breaking, so users should consider this before referencing the `latest` alias in a project.*
	
## Prerelease packages	
Another notation is used for publishing packages that are in a pre-release status or containing a critical bug fix which is not yet officially released by the author.  The sources for these packages are usually pulled from a named Github branch, so the branch name is included.  Also, despite not being part of a release yet, in order to allow for proper handling of semantic versioning the package will have a proper version number, which will be that of the next major release (even though it's not out yet).  An example of this notation is:

	Boost.Beast/1.66.0@bincrafters/git-develop
	
Much like testing, packages in these types of channels are considered volatile and not fit for production use.  When the next release of the package occurs, users testing this package should immediately switch to the stable branch.  After one month has passed with an official release, these pre-release packages are subject to removeal from the repository. 

## Feedback
If you have questions about the Bincrafters repository, please feel free to email us: bincrafters at g mail dot com

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 