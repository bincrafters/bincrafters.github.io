---
layout: post
title: 'Updated Conan Package Flow 1.1'
tags: [Conan.io]
---

In a [Previous Post](https://bincrafters.github.io/2017/11/10/Updated-Conan-Package-Flow/) we outlined the latest workflow for creating Conan packages for third-party open-source libraries based on some recent changes at that time.  Unfortunately, there were some problems with that workflow (and post), which are now rectified with today's release of Conan 1.1. Here's a primer on the latest process. 

---

## Biggest Change - Two Separate Workflows

After further discussion with the Conan team we realized there were two distinct types of packagers the client API was trying to accomodate: "in-source" and "out-of-source".  The Bincrafters packages are all built "out-of-source", meaning the `conanfile.py` is in a separate github repository from the library sources,  but one of the long-term goals of Conan is to foster the growing number of packages where the library maintainers manage the `conanfile.py` in their project ("in-source"). 

The previous updates were focused on "in-source" packaging workflows but it seemed it should be suitable for both scenarios. It did work, but it wasn't optimized, and came with a lot of unfortunate side-effects.  We brought this feedback to the Conan team and they aggressively sought various ways to accomodate our scenario and optimize our workflow. This brought about the recognition that the workflows are just fundamentally different, and some insight about possible solutions. 

## New Out-Of-Source Packaing Workflow 
So, the new workflow brings back the intuitive linear workflow that had prior to the November 2017 update.  After users have a `conanfile.py` that looks like it's ready to go, they can just jump right back to `conan create` as in:  

	$ conan create . bincrafters/testing

Most often, the `source()` method is pretty easy to debug and get right, and the first significant problems for debugging start occurring in the `build()` method.  So once we see that the `source()` method is getting the sources, we can move to the next stage of the workflow and focus on the `build()` method. Moving to next step of the workflow is as simple as adding `-k` to our command (short for `--keep-source`):

	$ conan create . bincrafters/testing -k
	
This step effectively replaces the `conan build` command/step that we previously recommended.  That command is still great for the in-source packaging workflow, but this approach comes with a bunch of advantages.  We won't go into them deeply, but in summary, it's simpler because `conan create` is idempotent, so it implicitly handles several steps that are otherwise manual, including cleaning up the `build` dir and copying fresh sources into it upon each run.  

So, after some amount of trial-and-error with the `build()` method, the package should eventually build the library properly. The next phase then becomes ensuring that the `package()` method is gathering all the proper files from the `build` directory.  This is often harder that it seems, and often requires trial and error also.  Obviously, the need here is to re-run the `package()` step multiple times, without re-running the `source()` or `build()` step.  And thus, this is exactly what the latest feature from Conan 1.1 enables.  We can now simply add `-kb` to our command (short for `--keep-build`): 

	$ conan create . bincrafters/testing -kb

The `-kb` flag also implies `-k`, effectively causing conan fast-forward to `package()` method and re-run it with whatever `build` directory has already been generated.  This was really the missing link for our "out-of-source" workflows before. 

The final step of the `conan create` command which often needs to be run many times until successful is the `test_package` step.  In this case, the best approach is to switch gears and actually take advantage of the separate and dedicated `conan test` command:

	$ conan test test_package bincrafters/testing

## Test Package Cleanup
	
Also regarding test_package, we got some great new features in Conan 1.1. One of the lingering problems for our team was that building packages always left behind the `test_package/build` directory in each package folder.  This directory has been almost completely useless the vast majority of the time (after the test_package is run), and so Conan has now given us a few flexible ways to clean this directory up automatically. 

1.  `CONAN_TEMP_TEST_FOLDER` - This is an environment variable that can be set to `True` to tell Conan to automatically cleanup the `test_package/build` directory automatically.  You can pass this variable to Conan via the CLI when you call `conan test` by adding `-e CONAN_TEMP_TEST_FOLDER=True`, but for most use cases, you probably want to set it in your default [Conan Profile](http://docs.conan.io/en/latest/reference/commands/misc/profile.html). 

2.  `temp_test_folder` - This is a value in `conan.conf` that you can set to have the same effect as the environment variable above.  The difference is that setting it in `conan.conf` is global, and will affect all recipes and profiles.  

3.  `--test-build-folder` - This is a flag to the `conan test` and `conan create` commands which allows you to specify a different `build` directory for the `test_package`.  This doesn't exactly help "automatically clean up" the directory, but it does allow you to choose to always put the `build` directory into some well-known temp directory rather than a subdirectory of your project folder.  This is a handy piece of flexibility. 
		   
## Summary
Again, it's important to point out that the recommendations here are for optimizing "out-of-source" builds, and that the previous post is still largely relevant for "in-source" builds.  However, for "out-of-source" builds which is still the majority of packages we see, this workflow brings a number of advantages.  

1. It's dramatically simpler, effectively only requiring knowledge of two Conan commands and two flags.  
2. It's inherently Idempotent, users don't have to manually create, specify, or delete any directories or files manually. 

We really hope other OSS packagers test this workflow for themselves and let us know their thoughts.  The Conan team is really amazing when it comes to listening to feedback, and we try to help encourage the feedback loop from the community for that reason.