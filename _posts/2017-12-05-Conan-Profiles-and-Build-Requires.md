---
layout: post
title: 'Conan Profiles and Build Requires'
tags: [Conan.io]
---

One highly under-discussed feature of Conan is it's flexible profile system. This post will demonstrate how to use these profiles to manage your build environment much more effectively than you could without, by allowing you to handle the build tools you use with Conan the same way you handle dependencies.  

## Profiles Primer
Conan does a lot of great things automatically.  For example, discovering what your environment has for building C and C++, and creating a default profile for it.  The discovery works so well, many people don't realize the profile system exists and is doing it's thing.  Nonetheless, every time you do something with Conan, it uses the information contained in the default profile to execute your build.  Once you know about profiles, you can specify a custom profile for each Conan operation via the CLI arguments.  You can list, read, and manipulate profiles (including the default) with the `conan profile` command, or you can simply edit them as text files under your home directory: 
	`.conan\profiles\`

## Build Tools Primer
If you're reading this you've probably used Conan a few times.  To do so, you needed to have a traditional installation of some common C++ build tools, installed in their default locations.  If it couldn't find some compiler such as GCC, Clang, MSVC, it probaly didn't work for you until it could. It turns out that "Traditional Installation + Conan Discovery" is all you need when you first start out, but eventually you will probably want more control and flexibility.  Many people want to use multiple compilers, and multiple versions of the same compiler, all on the same machine.  In these cases, managing these installations (and paths) manually can be challenging, especially when it comes to integrating with other build tools.  

## Build Requires Primer
Both the Conan team and the Bincrafters team have created a number of Conan packages which are not C or C++ libraries, but special "install packages" for these build tools. Examples of this include CMake, Strawberry Perl, Cygwin, MinGW, and more. When used, these packages don't "install" these tools exactly the way their normal installers do.  That would often involve permanently changing environment variables of the user or machine.  Instead, these packages are designed to extract all the files for the tool to the `package` subdirectory for that package in the local Conan cache.  Because such tools are encapsulated in individual, version-specific folders under the local cache, versions can exist side-by-side on the same machine without conflict.  Upon every execution of Conan, all the relevant environment variables and paths from these `build_requires` (for example `JAVA_HOME` or `MSYS_ROOT`) become set and available to Conan, but only for the scope of the current Conan operation. That is the key to the flexibility of this feature. 

## Profile + Build Requires
So, the magic here is that Conan profiles have a dedicated `build_requires` field of their own (independent of any recipe).  With this, Conan users can specify packages that get injected as `build_requires` for the current Conan operation (typicall `conan install ...`).  So, this lets the user choose between different versions of CMake, MinGW, or Java from one Conan operation to the next.  Equally important, **it doesn't require the users machine to have these tools pre-installed.**  **Conan automatically downloads and installs the tools as needed by virtue of it's normal package download functionality.**

## New Developers
Senior developers often have these problems well-tackled on their dev machines.  They might even have a complete series of VM's with a vast array of configurations and tools to rival a corporate CI infrastructure.  However, some developers might not (for example, junior developers trying to get into C and C++).  Thus, this feature can be a huge time saver for anyone who needs to build for multiple configurations, tools, and versions, but doesn't have (or doesn't want to continue to maintain) a complex environment with multiple parallel tools side by side on their dev machine.  

## Example
	
Here's an example of my default profile, where I've added `cygwin_installer` and `cmake_installer` as `build_requires`.  Now when I run Conan install or Conan create, it will automatically download Cygwin and CMake, extract them to directories in my local cache, and set the necessary environment variables to build with them.  Note that the `cmake_installer` package uses a unique version strategy, where the version of CMake is specified as an option to the package. Most other build tool packages use the tool version number in the package version number. 

```
[build_requires]
cygwin_installer/2.9.0@bincrafters/stable
cmake_installer/1.0@conan/stable
[options]
cmake_installer:version=3.8.2
[settings]
arch=x86_64
build_type=Release
os=Windows
compiler=Visual Studio
compiler.runtime=MD
compiler.version=15
[scopes]
[env]
```

## Bonus Example
The Conan team recently alerted me to another dimension of flexibility in the profile.  If you want to apply "cygwin_installer" and it's environment variables to only ONE package (for example "libcurl"), you can do so like this: 

```
[build_requires]
libcurl*: cygwin_installer/2.9.0@bincrafters/stable
```

Here is an example of a `package_info()` method from the `cygwin_installer` package. You can easily see what effect it has on environment variables.  
#### cygwin_installer ####
```
    def package_info(self):
        cygwin_root = self.package_folder
        cygwin_bin = os.path.join(cygwin_root, "bin")

        self.output.info("Creating CYGWIN_ROOT env var : %s" % cygwin_root)
        self.env_info.CYGWIN_ROOT = cygwin_root
        
        self.output.info("Creating CYGWIN_BIN env var : %s" % cygwin_bin)
        self.env_info.CYGWIN_BIN = cygwin_bin

        self.output.info("Appending PATH env var with : " + cygwin_bin)
        self.env_info.path.append(cygwin_bin)
```

## Current Build Tools Packages ##
Here is an informal list of all the build tools that you can now install with Conan simply by adding them to your profile: 

### Conan Center ###
* Strawberry Perl
* MinGW
* CMake
* 7Zip
* Nasm

### Bincrafters ###
* MSYS2
* Cygwin
* Bazel 
* GYP
* Ninja
* Java
* Yasm
* Ragel

## Note ##
Most native installers for build tools append their installed paths to the `PATH` environment variable, because it is often necessary for other tools which look for them.  Conan natively supports appending the PATH variable from the `pacakge_info()` method of a recipe.  However, there are currently some nuances with this in Conan.  For example, some variables need to be "appended", and some need to be "prepended".  Some tools that have filenames which conflict with others, such as `link.exe` and `bash.exe`.  There are other cases as well.  Thus, Bincrafters is currently working on a flexible strategy for handling these scenarios.  Once we have everything ironed out, we will have an option to update the `PATH` variable in a controlled way with our build tools packages. Ideally, this will be a feature added directly to Conan. 