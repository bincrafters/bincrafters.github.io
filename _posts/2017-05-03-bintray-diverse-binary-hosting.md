---
layout: post
title: 'Why we use Bintray'
tags: [bintray]
---

Perhaps one can guess from the similarity in our name, but Bincrafters was largely inspired by Bintray.  Unlike the other services we use such as Github, Travis, and Appveyor, there was never really anything quite like Bintray.  Also, as of this writing, there aren't any alternatives that provide anything close to what Bintray does: a mature platform for hosting a wide range of repository types, storing all of the binary types that we create and use, with all the of the modern management features we need: user management, a solid API, etc. 

## Hosting pacakges for the OS
Linux has had robust package management for many years, and in the past few Windows and Mac have both caught up.  Thanks to Bintray, we now have a single central place to host binaries compiled for all three major operating systems,  which can be downloaded and installed directly by the corresponding OS package manager.  The experience of external users who wish consume these binaries is extremely straightforward.  The experience of our developers for publishing to these repositories from their machines, or via CI services like Travis and Appveyor is also extremely easy, thanks in large part to lesser-known gem: the [JFrog CLI] (https://www.jfrog.com/getcli/)

## Hosting containers for Docker
DockerHub is the de-facto location for hosting public Docker containers.  This is not likely to change, however Bintray does offer docker hosting and in some cases there are at least a few compelling reasons why teams might choose to use Bintray instead of DockerHub.  One of which is the obvious advantage of a single place to hold many repos and binaries of many different types.  This is particularly helpful when you have to manage access for teams of developers. 

## Hosting for programming libraries
The Bincrafters team uses a wide variety of programming languages including C, C++, Go, Java, C#, Javascript, and others.  When working in teams and writing modular software, it's important to be able to quickly and flexibly create, distribute, and effectively version shared libraries.  Bintray lets us do this for all of the languages we use internally in a predictable way that's easy to introduce to new developers, and easy to manage. 

## Hosting for generic files such as sources
There are a great many binary files which don't have a proprietary repository type for storing them.  Two great examples are .zip and .tar.gz formats, used almost universally for storing source-code bundles.  Currently, a common option is to use github releases to store the zipped sources.  However, for projects which are setup to deploy compiled binaries to Bintray in other formats, for example a C++ library going to a Conan repository, or a Java library going to a Maven repository, it's trivial and valuable to add an extra line or two to also capture the sources and store them in a generic repository as well. 


[Bintray Homepage](http://bintray.com)
[Our Profile](http://bintray.com)
