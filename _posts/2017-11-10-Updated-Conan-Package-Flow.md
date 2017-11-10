---
layout: post
title: 'Updated Conan Package Flow'
tags: [Conan.io]
---

With the latest version of Conan, Bincrafters had to rethink our common workflows for developing packages.  We were a bit confused at first, and had to ask the Conan team for advice to get things streamlined. We wanted to share the current workflow with the community in case other packagers are also struggling to figure out the best flow with the updated command-line options.  

---

## Biggest Change - Save `conan create` for last

Previously, when you reached a point with a new recipe that you thought it was ready to "try", we would go straight to `conan create`, and run repeatedly until we had things working.  This is no longer the recommended approach, and there are some benefits with the new approach. At a high level, the `conan create` command was doing all its work inside your local cache directories, which was a bit non-trivial to find and browse to, and when starting a package, it's really not ready to go there anyway.  

## Testing a Recipe - Step by Step 
So, the new workflow encourages users to do trial-and-error in a local sub-directory relative to their recipe, much like how developers typically test building their projects with other build tools.  Also, the new strategy is to test the `conanfile.py` methods individually during this phase, which is something that was harder than it should have been in the past.  Below are the commands listed in the order we use them now: 

## `conan source`
Now, you will generally want to start off with the `conan source` command, for example: 
	$ conan source . --source-folder=tmp/source

The strategy here is that you're testing your source method in isolation, and downloading the files to a temporary sub-folder relative to `conanfile.py`.  This just makes it easier to get to the sources and validate them.  Once you've got your source method right, and it contains the files you expect, you can move on to testing the various attributes and methods relating to the downloading of dependencies. 

## `conan install`
Conan has multiple methods and attributes which relate to dependencies (all the ones with the word `require` in the name). The command `conan install` activates all them:
	
	$ conan install  . --install-folder=tmp/build --profile XXXX

This also generates `conaninfo.txt` and `conanbuildinfo.xyz` (extension depends on generator you've used) in the temp folder, which will be needed for the next step.  Once you've got this command working with no errors, you can move on to testing the `build()` method. 
	
## `conan build`
The build method takes a path to a folder that has sources (basically an "input" dir), and a path to a folder where it will perform the build (basically an "output" dir).  
	
	$ conan build . --source-folder=/tmp/source --build-folder=/tmp/build

This is pretty strightforward, but it does add a very helpful new shortcut for people who are packaging their own library. Now, developers can make changes in their normal source directory and just pass that path as the `--source-folder`.  It does seem more sensible in that workflow. 

## `conan package`
Just as it sounds, this CLI command now simply runs the `package()` method of a recipe. Like the `conan build` command, it basically take "input" and "output" paths, in this case `--build_folder` and `--package_folder`. 
	
	$ conan package . --build_folder=tmp/build --package_folder=tmp/package

## `conan create` 
Now we know we have all the steps of a recipe working. Thus, now is an appropriate time to try to run the recipe all the way through, and put it in the local cache.  

	$ conan create user/channel

## Summary
There were other Conan command changes which affect other workflows, but we only wanted to focus on what we felt to be the most common OSS workflow for authoring and testing packages for third-party libraries.  We hope this helps, and if you have any shortcuts or tips (or we've documented something wrong here), please feel free to reach out to us on twitter, email, slack, or github. 