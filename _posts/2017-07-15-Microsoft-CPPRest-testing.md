---
layout: post
title: 'Microsoft CPPRest SDK Conan Package - Available for Testing'
tags: [C++, Conan.io]
---

A new package is now available on the Bincrafters `public-conan` repository: Microsoft's "CPPRest SDK".  Formerly known as "Casablanca", the CPPRest SDK is one of the most stable and mature REST libraries for C++.  It is a solid library for interacting with any REST API, not just those provided by Microsoft.  For instructions on using Bincrafters `public-conan` repository, [please see this post](2017-06-06-using-bincrafters-conan-repository.md).

Package reference: 
	$ cpprestsdk/2.9.1@bincrafters/testing

---

## Use Cases
Notably, it supports websockets, and the [Swagger project](https://swagger.io) has a [generator for the CPPrest SDK](https://github.com/swagger-api/swagger-codegen/tree/master/samples/client/petstore/cpprest), which will automatically generate the C++ library code for any API you wish to use if that API has a published "swagger spec".


## Status - Testing
Currently, these packages do not yet have a `stable` branch, however we expect to have that completed soon.  In the meantime, we are looking for beta testers to use the packages on the `testing` branch, but with the disclaimer that it should not be used for production code, and is subject to change at any time.  If you do test and have feedback, please open an issue on the github repository for this recipes project.  http://github.com/bincrafters.