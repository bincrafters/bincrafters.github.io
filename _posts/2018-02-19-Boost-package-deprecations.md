---
layout: post
title: 'Announcement: Boost package deprecations'
tags: [C++, Conan.io, Boost, Bintray]
---

This is an announcement of the planned deprecation and replacement of the Bincrafters modular boost packages. Specifically, the boost modular packages for v1.64.0 and v1.65.1 featuring upper-case characters and dots will be removed.  Users must switch to the new naming convention featuring all lower-case characters and underscores. 

## Example  

**Old:** `Boost.System/1.66.0@bincrafters/stable`  
**New:** `boost_system/1.66.0@bincrafters/stable`  

## Required Action  
For the `boost` packages, users should begin migrating their package references to point to the new naming convention ASAP.  Also of note, the `boost` packages were completely re-written during the rename, with a number of patches and bugfixes.  If you discover a breaking change to your setup, please let us know (see github issues link at the bottom of this post).  
	
## Timeline  
On **3/15/2018**, the old Boost modular packages with upper-case characters in the name will be removed from Bintray.  Any local cache containing the packages will continue to work as long as the user does not clean said cache. The old github repositories containing the old recipes will also be removed on **3/15/2018**. 

## Reasoning  
The overwhelming majority of Bincrafters packagers and community members agreed that establishing and following a convention of lower-case-only package names was preferred.  As Conan has just come out of Beta, and we were preparing the packages for submission to Conan Center, we decided that now was our last opportunity to make this change, which we would be living with for years to come.   

## Issue Reports and Feedback  
As usual, please let us know if you have any trouble with the new packages on our Github Community Issues list: 

[https://github.com/bincrafters/community/issues](https://github.com/bincrafters/community/issues)

Thanks again to the community members who have submitted feedback and issues so far.  It has substantially improved the quality and direction of Bincrafters, and we hope to continue to see this kind of collaboration. 