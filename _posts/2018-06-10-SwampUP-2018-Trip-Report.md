---
layout: post
title: 'SwampUP 2018 Trip Report'
tags: [Conan.io]
---

JFrog's swampup conference 2018 happened last month, and the devops challenges of C and C++ received a great deal of attention.  There was a Conan training session on Day 1, a Conan roadmap discussion on Day 2, and a room dedicated to Conan talks on Day 3.  This trip report is focused primarily on sharing the predominant themes and feedback heard from the swampup attendees who came to these events to learn and talk about C and C++.  

---

### About the Conference Itself

In general, I have to say that this was one of the most well-organized and enjoyable conferences I've ever been to. I see why people who come once, tend to return each year thereafter.  The attribute about this conference which was probably the most unique and memorable was the diversity of technology represented for such a small conference.  It was not dominated by a single vertical, language, cloud platform, or even a specific devops concept like containers.  We had experts talking about every part of devops, from a vast array of companies and ecosystems. 

### Conan Audience - The Enterprise  

There were a few clear message among the Conan audience about devops for C and C++.  One such message was that the open-source ecosystem is only part of the story of dependency management.  Another was that enterprise devops teams and workflows need and want a solution which manages and deals with compiled binaries, and not just sources.  These might be the most important takeaways from the conference to be highlighted for the wider C and C++ community, and particularly anyone people involved with the C++ committee study group SG15.  Understanding the perspectives of the large enterprises who are aggressively pursuing "package management" seem very relevant to the process of creating any successful standards in the realm of tooling interoperability.  

Also of note, the package management discussions contained a lot of substance in the form of concrete details about homegrown devops strategies these companies have tried in the past, along with feedback about the costs, benefits, and lessons learned from those strategies. The conference really shined light on the under-representation of this enterprise user base in the public discussion around tooling and how unfortunate that is given that this user base contains extremely wise and experience build engineers.  

### Enterprise Characteristics

The enterprise devops engineers had several things in common.  

- Mix of proprietary and open-source code
- Diverse, proprietary build systems and/or scripts
- Large, decentralized dev teams
- Continuous Integration
- Cross Compiling

A few additional notes: virtually everyone was using some form of CI servers such as Jenkins to automate tests and builds, only a few were using docker for C and C++, and only a few were using CMake as a primary build system.  To be fair, most didn't seem to have a "primary" build system at all, because most had to support several in parallel. 

### Roadmap Discussion

There was an interesting meeting where engineers from many of the existing and potential companies using Conan gathered to vote on potential roadmap features.  This was not to dictate the course of the future, but rather to gather and weigh feedback.  There were 15 proposed items taken from existing feature requests.  There were a few that stuck out as being relevant to Bincrafters, so we'll focus on those. 

#### Python Code Sharing

Codesharing of python code using Conan rather than PIP was one such feature.  This had been boiling up in the slack channel in the days leading to the conference, so it was no surprise that it was front and center in the meeting.  @grafikrobot from the bincrafters team had to do extensive work to implement this kind of functionality manually for the boost recipes, so this one definitely has value for us.  It was pretty unanimous among the rest of the group, and with a "prototype" already sketched out by the Conan team, this one seems to be imminent.  This will probably be easiest win.  

#### Conan Source Method

The discussion around features related to new options for dealing with source code was an interesting one. It seemed to be important to a few people, but it was not a feature request we had seen in the community previously.  The specific proposal was to bring process of obtaining sources for each build from GIT at build time to the local development flow (which traditionally uses the exports_sources feature instead of a source method).  It also included implicitly locking a Conan package version to the GIT commit hash that was the HEAD at the time Conan was first called on the target recipe.  There were other related requests around the sources for packages.  Some were concerned about the sources being zipped up in the packages being a liability.  Meanwhile, we've had cases in Bincrafters where we wanted the opposite (to bundle sources in packages which use the source method to fetch external sources at build time).   One common theme was that pretty much everybody was trying to work toward reproducible builds which is good.  Despite the interest in the she specific feature proposed, there are some substantial challenges to implementing this functionality, so you probably shouldn't expect to see this come out any time soon.

#### Conan Workspaces (Conan Project)

Different names have been kicked around for this feature, but we'll call it workspaces for now.  In short, it's a feature designed to make it more familiar and slightly more efficient for developers to leverage Conan while editing multiple inter-dependent projects at the same time.  Really this feature is about enabling developers to use the same pattern of temporary build directories their projects are setup to use today (and thus less refactoring and re-training), and also to skip the potentially un-necessary copies of sources and binaries to the Conan cache, which occurs regularly when builds are run through Conan.  With this feature, users can define a YAML file in a directory structure that Conan discovers, and which tells Conan how these project folders are laid out in the user's workspace.  Based on the definitions in the file, Conan points to the appropriate temporary build directories for the compiled binaries when generating `conanbuildinfo` files (rather than the Conan cache).    Much like python code sharing, there's an active prototype of this feature with many users interested in it, so it seems imminent. 

#### Package Revisions

Package revisions was probably the second most significant feature for Bincrafters, and the problem goes back as far as the existence of binary package managers, and still poses problems for extremely mature package managers such as APT and YUM.  If you're not familiar with this one, there are two known challenges surrounding semantic versioning with packages, one of which affects the OSS world, the other affects the enterprise.  

In the OSS world, the challenge is meeting three conflicting objectives with nothing but a version field.  Most everyone wants to maintain the existing versioning strategy because it is the most intuitive, whereby we use the version number from the upstream library as the version number for the package.  However, the first competing objective is the widespread desire for package immutability.  This is the principle that once a public package is uploaded to the official central repository, the binaries should not change for any reason, lest a "fix" or improvement might actually break users who have already worked around the bug or deficiency themselves.  The last part of the conflict is the fact that there is no such thing as a perfect package with C and C++, and there are numerous valid reasons to update a package, even when in the central repository. While everyone agrees that we would prefer not to overwrite existing in-use binaries, there's no good alternative when there's a severe problem with a binary. There are proposed mitigations, but are all undesirable, as they all sacrifice something without even solving the whole problem.   It's widely agreed that the best solution is a new first-class feature designed to solve this problem specifically, however the specifics of how it would work have yet to be determined, let alone tested and validated. 

In the enterprise world, there's a different problem.  Many C and C++ codebases don't use semantic versioning for their internal modules.  The term "live-at-head" coined by Titus Winters at CPPCon 2017 describes a strategy that is very common in C and C++, where developers all work off a super repo that contains all the modules, and they're effectively "versioned together" by virtue of the source control system.  In simple terms, the conclusion by many enterprise build engineers is that trying to migrate from this approach to any manual versioning strategy is a huge source of complexity, a burden to developers, and will be a constant source of problems.  In the wide world of open-source software, this burden is absolutely necessary and warranted, but in enterprise development it's often not.  In these types of environments, it seems clear that we should be using the same strategy as source control systems, with hashes with timestamps that are completely automatic, yet still traceable. Furthermore, many organizations need to be able to correlate source control changes to specific binaries that were built from them. Achieving this in the current version of Conan involves a lot of manual engineering but could be done much more elegantly by adding automatic versioning features to Conan, along with a few others. 

For Conan, the overarching challenge to providing all of these options is that the traditional strategy of manual version management has been baked into the core logic of the platform from day one, and countless other features rely on it to work a certain way.  It's overwhelming to try to imagine how to implement an alternative system which contains several potential implicit behaviors, and still works with all the packages and recipes which exist today.  

The good news is that concept of "package revisions" (as discussed at a high level) seemed like it could address both cases.  The current idea is basically an implicit "revision" field incremented and applied automatically upon each build, which exists in addition to manually specified version.  Package queries would then default to a "latest revision" behavior, with simple and familiar ways of changing the behavior to "oldest" or locking on specific revisions.  The bad news is that this feature is extremely far away because of its overwhelming nature.  At best, we might hope to see it in beta as part of 2.0, but even that seems uncertain, and we probably won't see a 2.0 release until 2020 anyway.  

### Summary

Once again, it was a great conference, and that the discourse among the enterprise C and C++ engineers was invaluable to me as a Bincrafter, and it was certainly invaluable to the Conan team as well.  We truly hope that this trip report will also start to shine more light on the importance of understanding and accommodating both OSS and enterprise use cases in Conan, as well as other parts of the tooling ecosystem like build systems, and CI services. 