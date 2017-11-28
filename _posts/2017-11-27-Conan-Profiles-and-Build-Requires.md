---
layout: post
title: 'Conan Profiles and Build Requires'
tags: [Conan.io]
---

One highly under-discussed feature of Conan is it's flexible profile system. This post will demonstrate how to use these profiles to manage your build environment much more effectively than you could without, by allowing you to handle the build tools you use with Conan the same way you handle dependencies.  

## Profiles Primer
Conan does a lot of great things automatically.  For example, discovering what your environment has for building C and C++, and creating a default profile for it.  The discovery works so well, many people don't realize the profile system exists and is doing it's thing.  Nonetheless, every time you do something with Conan, it uses the information contained in the default profile to execute your build.  Once you know about profiles, you can specify a custom profile for each Conan operation via the CLI arguments.  You can list, read, and manipulate profiles (including the default) with the `conan profile` command, or you can simply edit them as text files under your home directory: `.conan\profiles\`

## Build Tools Primer
So, if you're reading this you've probably used Conan a few times.  To do so, you needed to have a traditional installation of some common C++ build tools, installed in their default locations.  If it couldn't find some compiler such as GCC, Clang, MSVC, it probaly didn't work for you until it could. It turns out that "Traditional Installation + Conan Discovery" is all you need most of the time, however not all the time.  Many people want to use multiple compilers, and multiple versions of the same compiler, all on the same machine.  In these cases, managing these installations (and paths) manually can be challenging, especially when it comes to integrating with other build tools.  

## Build Requires Primer
Both the Conan team and the Bincrafters team have created a number of Conan packages which are not C or C++ libraries, but special "install packages" for these build tools. Examples of this include CMake, Strawberry Perl, MinGW, MSYS, Cygwin, Bazel, Java, and more. When used, these packages don't "install" these tools exactly the way their normal installers do.  That would often involve permanently changing environment variables of the user or machine.  Instead, these packages are designed to extract/install all the files for the tool to the `package` subdirectory for that package in the local Conan cache.  Because such tools are encapsulated single version-specific folders under the local cache, versions can exist side-by-side on the same machine without conflict.  Upon every execution of Conan, all the relevant environment variables and paths from these `build_requires` (for example `JAVA_HOME` or `MSYS_ROOT`) become set and available to Conan, but only for the scope of the current Conan operation. That is the key to the flexibility of this feature. 

## Profile + Build Requires
So, the magic here is that Conan profiles have a dedicated `build_requires` field of their own (independent of any recipe).  With this, Conan users can specify packages that get injected as `build_requires` for the current Conan operation (typicall `conan install ...`).  So, this lets the user choose between different versions of CMake, MinGW, or Java from one Conan operation to the next.  Equally important, **it doesn't require the users machine to have these tools pre-installed.**  **Conan automatically downloads and installs the tools as needed by virtue of it's normal package download functionality.**

## New Developers
Senior developers often have these problems well-tackled on their dev machines.  They might even have a complete series of VM's with a vast array of configurations and tools to rival a corporate CI infrastructure.  However, some developers might not (for example, junior developers trying to get into C and C++).  Thus, this feature can be a huge time saver for anyone who needs to build for multiple configurations, tools, and versions, but doesn't have (or doesn't want to continue to maintain) a complex environment with multiple parallel tools side by side on their dev machine.  

## Example
	
It's very simple.  Here's an example of my default profile, where I've added `cygwin_installer` as a `build_requires`.  Now when I run Conan install or Conan create, it will automatically download Cygwin and set the necessary environment variables to build with it:

```
[build_requires]
cygwin_installer/2.9.0@bincrafters/stable
[settings]
arch=x86_64
build_type=Release
os=Windows
compiler=Visual Studio
compiler.runtime=MD
compiler.version=15
[options]
[scopes]
[env]
```

Below is the `package_info()` method from the recipe for the Cygwin package. You can easily see what environment variables it sets.  

```
    def package_info(self):
        ...
	    self.env_info.CYGWIN_ROOT = self.package_folder
	    self.env_info.CYGWIN_BIN = os.path.join(self.package_folder, 'bin')
```
