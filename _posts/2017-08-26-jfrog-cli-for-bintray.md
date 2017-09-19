---
layout: post
title: 'Using the JFrog CLI for Bintray'
tags: [Bintray]
---

The JFrog CLI can be used with all of JFrog's products: Artifactory, Bintray, Mission Control, and Xray.  This post focuses on it's usefulness to Bintray users who are in the business of packaging and uploading binaries on a regular basis. 
 
---

## Continuous Integration
Appveyor and Travis-CI both have direct support for uploading artifacts to Bintray (among other destinations).  They allow users to define the specifics of the uploads in their respective .yml files, which has the advantages of being a declarative way to specify the upload.  This subtle disadvantage of this approach however becomes apparent for power users who are working rapidly and creating and modifying recipes regularly.  It's the same problem with the rest of the Travis and Appveyor recipes: local reproducability.  

## Build Logic in .yml files
Many developers who have worked with these CI systems for a little while come to the same conclusion, that build scripts are best kept contained in script files which can be executed locally, and then simply call those from the CI files, reducing the CI step to a single call to a script with no arguments (everything passed through environment variable.)  It seems to negate some of the objectives of these CI systems, with their approach of .yml files where developers are supposed to define commands as lines in an array.  However, the evidence that this is impractical for non-trivial builds is fairly overwhelming at this point, and the same conclusions hold for the upload step as well.  

## The JFrog CLI
The CLI provides a consistent interface and scripting API across developer machines of any operating system, Appveyor, and Travis-CI.  It can be installed in any of these places with just a single command, making it a very easy tool to adopt and integrate into a process.  Furthermore, it supports the massive range of file and repository types supported by the Bintray platform, so it can be used to push Nuget, Maven, Debian, Redhat, MSI, ZIP, TAR.GZ, Docker, and other binary formats alike.  It's a powerful tool and highly valuable in the toolbox of almost any developer who uses Bintray. 