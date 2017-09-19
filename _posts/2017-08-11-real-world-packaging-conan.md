---
layout: post
title: 'Real-World Packaging C++ with Conan.io'
tags: [Conan.io, C++]
---

Over the past year, each member of the Bincrafters team has worked extensively with the Conan platform on packaging a diverse array of C and C++ libraries.   We've had the opportunity to dig very deep into advanced features such as custom generators, conan package tools for CI automation, and a great deal of debugging.  Here are some of the things we've learned about advanced packaging at scale.  

* Header-Only Libraries - Cut the settings and options, use the special `package_id()` for header-only libs.
	[Example](https://github.com/bincrafters/conan-boost-assert/blob/cc0f1b2ae0684a55425abceb8a03508a258ae86f/conanfile.py#L26)

* Third-Party CMake Libraries - Inject the template content in the CMakeLists.txt file of the target project. 
	[Example](https://github.com/bincrafters/conan-azure-umqtt-c/blob/4134dc0b99bf25395dda6e58dacc2b5a71c0024d/conanfile.py#L28)
	
* CMake - Use the built-in CMake helper rather than doing self.run(cmake...)



* Favor Archives over Git Clone When Possible - Both have pros and cons, Obviously, sometimes git is required. 

* Need to do something clever or tricky? Wait...
	* Search the docs for keywords
	* Search github.com/conanio/conan/issues
	* Look through github.com/lasote and github.com/memsharded for recipes 
    * Search for other examples by github searching "conanfile.py" and some keywords
	* Always check the conan docs for the helper methods on the `tools` class. 
	* Come to cpplang.slack.com (https://cpplang.now.sh) and ask in the #conan channel

* Just use stable/testing channels unless you have a good reason for something else. If you see others like "release" and "ci" , those are older and no longer favored. 

* For git branch names, once you grow out of `master` use the convention  `channel/version` as in `stable/1.64.0`

## repeated testing while creating first packages
Use `conan create <user/channel>` to try to build your recipe for the first time.  However, once you are sure you've got the `source()` method working right, do `conan create <user/channel> -v`. This will skip the source() method so you don't redownload the sources over and over, saves lots of time.   

## test_package
Only validate the bare minimum, it's not another unit test.  Just link and/or include from the library. For example, simply instantiate a class.  test_package   Also, make your test_package files as generic as possible.  You don't need any unique information in the test_package folder outside of the content in the .cpp file. 
[Example](https://github.com/bincrafters/conan-boost-system/tree/stable/1.64.0/test_package)

## `build_requires()`
This is also a very important feature for packaging C and C++, which often have strange requirements.  If a project has preconditions for the machine being built, `build_requires` can probably help with that.   You can make a package that can setup anything on the machine, from installing CMake to [Simply downloading and installing Strawberry Perl to build OpenSSL](https://github.com/lasote/conan-strawberryperl/blob/52f88299851958c58c1997dde3a3084834f00577/conanfile.py#L29).  Here you can see the use of the PATH.APPEND().  So, the OpenSSL recipe `build_requires` the Strawberry Perl recipe, which means it will get the "APPENDED" "PATH" variable, and therefor be able to call perl.exe successfully in it's own `build()` method. 