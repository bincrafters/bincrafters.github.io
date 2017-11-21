---
layout: post
title: 'Conan Package - Microsoft C++ REST SDK'
tags: [C++, Conan.io, Bintray]
comments: true
---

Bincrafters has now published a Conan package for Microsoft C++ REST SDK to our public Conan repository on Bintray. It is a project which offers both HTTP client and server functionality, including websockets support.  It features a modern asynchronous API design in C++ with Boost Asio.  It is cross-platform, supporting Windows, Linux, and Mac, as well as IOS and Android.  The C++ REST SDK is widely used among C++ projects which have need to interact with REST services.  [A swagger generator for the C++ REST SDK](https://github.com/swagger-api/swagger-codegen/tree/master/samples/client/petstore/cpprest) has also been constructed by the community, which can generate the C++ code needed to compile a strongly-typed C++ SDK for any REST API that publishes a swagger specifications.  This makes it an obvious choice for interacting with any such REST API. 

## Package Reference

    cpprestsdk/2.9.1@bincrafters/stable
    
## Usage Information  

To get started with using the Bincrafters public Conan repository, please see this post:
[Bincrafters Conan Instructions](https://bincrafters.github.io/2017/06/06/using-bincrafters-conan-repository)

## Notes About this Package 

You can get more details from [the README on github](https://github.com/bincrafters/conan-cpprestsdk)

This package builds upon a number of other open source C and C++ libraries including OpenSSL, Boost, and WebsocketPP.  All dependencies come from either Conan Center or the Bincrafters public Conan repository. 

### Package Options
Conan allows users to pass options to for each package upon install. The list of options for this packages is included below: 

|Option Name	  | Default Values   | Possible Value  | Description
|----------------|-------------------|-------------------|-------
|shared           | True                 | True/False       | Use as a shared library or static library


## Status - Stable
This package has been tested and is currently considered stable.  Please report any issues through the github repository for this recipe. 

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 
