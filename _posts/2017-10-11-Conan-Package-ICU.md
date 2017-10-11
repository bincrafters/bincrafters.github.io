---
layout: post
title: 'Conan Package - ICU'
tags: [C++, Conan.io, Bintray]
---

Bincrafters has now published a Conan package for IBM's open-source libraries known as "ICU" to our public Conan repository on Bintray. ICU stands for "International Components for Unicode" and is a mature and portable set of libraries for software internationalization (I18N) and globalization (G11N) which implement the Unicode® Standard, giving applications the same results on all platforms."

ICU has been used for decades in C and C++ libraries and applications to handle unicode.  Major frameworks such as Boost and Qt both use it in various modules. 

## Package Reference

    icu/59.1@bincrafters/stable
    
## Usage Information  

To get started with using the Bincrafters public Conan repository, please see this post:
[Bincrafters Conan Instructions](https://bincrafters.github.io/2017/06/06/using-bincrafters-conan-repository)

## Notes About this Package 

You can get more details from [the README on github](https://github.com/bincrafters/conan-icu), but 

### Package Options
Conan allows users to pass options to for each package upon install. The list of options for this packages is included below: 

|Option Name		 | Default Values   | Possible Value                      | Description
|---------------------|-------------------|----------------------------------------------------------
|shared					 | True                  | True/False                            | Use as a shared library or static library
|with_io				 | False                 | True/False                            | Compile the ICU Ustdio/iostream library
|with_msys			 | False                 | True/False                            | Supplies the MSYS Conan package to use at build time
|with_unit_tests	 | False                 | True/False                            | Run the ICU unit tests before compiling
|with_data			 | False                 | True/False                            | Build the ICU sample data with default settings. 
|msvc_platform	 | visual_studio     | visual_studio, cygwin, msys  | Choose a compiler front-end
|data_packaging	 | archive             | shared, static, files, archive   | See [ICU Data Packaging documentation](http://userguide.icu-project.org/packaging)



## Status - Stable
This package has been tested and is currently considered stable.  Please report any issues through the github repository for this recipe. 

## Disclaimers
Prior to using Bincrafters packages, please see the [Bincrafters Disclaimer Page](https://bincrafters.github.io/2017/05/01/bincrafters-package-disclaimers/). 