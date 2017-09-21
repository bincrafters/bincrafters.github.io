---
layout: post
title: 'Command-Driven Toolset for OS Packaging - In Go, By mh-cbon'
tags: [Bintray, Cross-Platform]
---
A github user known as @mh-cbon has created a wonderful set of tools for packaging and general release management.  They are all written in Go, but they are all built and packaged as native binaries used at the CLI, so they can be used to package and release software written in any language.  The toolset can be found here: 

https://github.com/mh-cbon/go-github-release

## Core Tools
At the center of the toolset and it's value are the three packaging executables: 
* [go-bin-deb](https://github.com/mh-cbon/go-bin-deb) - A Facade 
* [go-bin-rpm](https://github.com/mh-cbon/go-bin-msi)
* [go-msi](https://github.com/mh-cbon/go-msi) (creates both msi and nuget) 

## Core Overview
These three tools provide a uniform process for taking whatever files you need to package, and producing the output file of the corresponding package type.  The uniform process involves a friendly json config file for each, and supports the passing of other necessary options at the CLI.   It's hard to overstate the subtle brilliance of the solution here.  The author has taken four separate workflows and toolsets, where the documentation and API's among them seemed vastly different and unreconcilable, and unified them into a single simple and consistent workflow.   It's worth noting however, that there still seems to be no way around the requirement that you have to be on the OS for which you want to package, and have the tools installed.  `go-msi` requires wix or nsis, `go-bin-rpm` requires all the rpm tools be installed and run on a redhat/centos/fedora machine, and `go-bin-deb` requires build-dep be installed and run on a debian or ubuntu machine. 

## Additional Tools
On the periphery are some other tools which are elegant in their own right:
* [emd](https://github.com/mh-cbon/emd) - enhanced markdown for automating readme updates
* [changelog](https://github.com/mh-cbon/changelog) - parses git logs to automatically build a changelog, multiple format outputs
* [gump](https://github.com/mh-cbon/gump) - lets users specify multiple command to run every time a version bump is done

Although it's not required to use these tools, there are some integrations among the toolset.  In general, these tools are broadly useful for anyone trying to manage a software release pipeline with a team, especially if there are multiple languages and toolsets at work. 

## Summary
The toolset brings to light a few valuable insights.  
1. Small, native, cross-platform, command-driven tools can provide unique utility and broad applicability for developer tools from all ecosystems.  Git is another such tool that demonstrates this point well.  
1. While there are many packaging tools which are integrated into toolsets that are specific or proprietary to a particular development ecosystem or operating system, having a toolset where each tool can stand on it's own again provides unique value.  
1. Go has several libraries which together provide a good experience for creating small command-driven utilities.  