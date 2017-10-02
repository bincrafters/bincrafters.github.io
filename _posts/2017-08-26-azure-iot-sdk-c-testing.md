---
layout: post
title: 'Conan Package - Azure IOT SDK for C - Available for Testing'
tags: [C++, Conan.io]
---

A new package is now available on the [Bincrafters Public Conan Repository](https://bintray.com/bincrafters/public-conan): "The Azure IOT SDK for C" published by Microsoft.  It is a pure C library for communicating with Microsoft Azure's IOTHub platform, and features a collection of other pure C libraries for things like MQTT, AMQP, JSON Parsing, etc.  Each library is packaged separately with Conan, and the dependency tree is expressed appropriately in each recipes. For instructions on using these libraries from our repository, [please see this post](2017-06-06-using-bincrafters-conan-repository.md).

## Package reference: 
```
[requires]
Azure-IoT-SDK-C/1.1.21@bincrafters/stable
```
---

**Update 9/18/2017 - We've Recieved Positive Feedback from Microsoft**
A while ago, we made the announcement of the library via a github issue on the IOT SDK repository on the hopes that someone in the Microsoft team or the user community would find them of use or interest.  We just received some positive feedback so we should definitely be continuing to improve these recipes for the forseeable future.  

[Read the comments here](https://github.com/Azure/azure-iot-sdk-c/issues/226)

Also, we put together [this demo of using Azure IOT SDK via Conan].(https://github.com/bincrafters/azure-iot-sdk-demo-conan)

## Use Cases
The "The Azure IOT SDK for C" is tailored for Microsoft's platform, so if you're interested in this platform and use Conan already, then this Conan package is just an easier way to consume it than using "git" and compiling it manually as indicated by the Azure IOT SDK team.  However, the other libraries that it depends on are generic enough that they should be usable in other C projects.  Particularly the MQTT and AMQP libraries, which are fundamental communication protocols for IOT.  JSON parsing is also a very common and practical operation in an IOT device, so that library could also prove valuable.  Again, because we've packaged those components separately, you can consume them a-la-carte. 

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 
