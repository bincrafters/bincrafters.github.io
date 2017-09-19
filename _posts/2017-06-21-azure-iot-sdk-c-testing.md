---
layout: post
title: 'Azure IOT SDK for C - Available for Testing'
tags: [C++, Conan.io]
---

A new package is now available on the Bincrafters `public-conan` repository: "The Azure IOT SDK for C" published by Microsoft.  It is a pure C library for communicating with Microsoft Azure's IOTHub platform, and features a collection of other pure C libraries for things like MQTT, AMQP, JSON Parsing, etc.  Each library is packaged separately with Conan, and the dependency tree is expressed appropriately in each recipes. For instructions on using Bincrafters `public-conan` repository, [please see this post](2017-06-06-using-bincrafters-conan-repository.md).

* Package reference: 
```
[requires]
Azure-IoT-SDK-C/1.1.21@bincrafters/testing
```
---

## Use Cases
The "The Azure IOT SDK for C" is tailored for Microsoft's platform, so if you're interested in this platform and use Conan already, then this Conan package is just an easier way to consume it than using "git" and compiling it manually as indicated by the Azure IOT SDK team.  However, the other libraries that it depends on are generic enough that they should be usable in other C projects.  Particularly the MQTT and AMQP libraries, which are fundamental communication protocols for IOT.  JSON parsing is also a very common and practical operation in an IOT device, so that library could also prove valuable.  Again, because we've packaged those components separately, you can consume them a-la-carte. 


## Status - Testing
Currently, these packages do not yet have a `stable` branch, however we expect to have that completed soon.  In the meantime, we are looking for beta testers to use the packages on the `testing` branch, but with the disclaimer that it should not be used for production code, and is subject to change at any time. 