---
layout: post
title: 'Conan Packages - Boost v1.66.0'
tags: [C++, Conan.io, Boost, Bintray]
---

Finally.... 
For two months, Bincrafters has been refactoring and refactoring on the Boost 1.66.0 packages, and they're finally ready for consumption.  In case you're new to Bincrafters, here's the link to our repository: 
[Bincrafters Public Conan Repository on Bintray](https://bintray.com/bincrafters/public-conan)

## Usage Notes
There are ~135 libraries in Boost, so obviously there are a few nuances related to the packages which users might want to know.  We've created a page in our documentation to capture all these usage details, and will continue to add to it over time.  

[Usage Notes for Boost Packages](http://bincrafters.readthedocs.io/en/latest/package_notes.html#boost)

Here are some highlights: 
- `FindBoost.cmake` : CMake refs to Boost::xyz and Boost_FOUND now work
- `all` : bugfixes... bugs and important flags fixed everywhere
- `all` : packages now built with both libcxx options (libstdc and libstdc++11)
- `boost_iostreams` : zlib, bzip2, and lzma compressors are enabled by default 
- `boost_python` : improved version and python path detection. better override options.
- `misc` : C++11 Only Libraries include: `log`, `context`, `coroutine`, `fiber`


## Backporting
We are currently in the process of rebuilding 1.65.1 and 1.64.0 with the new changes.  We hope this will be ready by 2/20/2018.   