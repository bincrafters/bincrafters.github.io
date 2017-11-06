---
layout: post
title: 'Bincrafters Status Update'
tags: []
---

We've received a lot of really great feedback from the C++ community about the Conan packages we've been publishing over the past few months. We are really grateful to the community and the Conan team for the support, and we had a few other updates we wanted to share. 

---

## Packaging Poll Results

Recently, we posted an open poll on Pollly.com, asking what packages users wanted to see.  Here's a link to the poll, followed by a summary of the results. 

[https://poll.ly/#/2qBaRenB](https://poll.ly/#/2qBaRenB)

The poll will continue to remain active, and will continue to watch to see if any new ones rise to the top.  We may very well package some of those libraries with only 1-3 votes, we just wanted to get the pulse of whatever community the poll was able to reach. 

### Qt
Qt was at the top of the list, which is unlikely to surprise anyone.  For those interested, we WILL be packaging Qt, and we will be attempting to modularize everything just as we did with Boost.  

As for a timeline, we can't begin to provide one yet.  The size and complexity of the project appears to be on par with the packaging of Boost, which took a group of us about 3 months to get right. Also, with Boost we had the distinct advantage of having a member of the team who is one of the foremost experts in the building of the boost libraries: @grafikrobot. Currently, we don't have anyone from Qt on the team. We also don't know what sorts of beasts await us on that journey.  Even with Boost we had plenty of surprises, so it would be naive to think Qt will go any differently. 

### Other Packages From Poll
The poll also really gave us a good indication of where to focus future efforts as well.  In fact, several of them had already been completed and just not publicized, others were in progress, and others are now on our backlog.  Unfortunately, Pollly doesn't have any advanced features like adding a note/comment or marking anything as complete, so here are some updates:

|Complete        |In Progress      |On Horizon          |
|---------------|----------------|------------------|
|RxCPP            |   libcurl           |  libjson        
|fmtlib             |  grpc              | libcrypto
|websocketpp   |  protobuff      | botan
|cpprestsdk      |  zeromq        | sqlite
|                     |                     | tensorflow
|                     |                     | glm
|                     |                     | sqlite
|                     |                     | crypto++
|                     |                     | folly
|                     |                     | libtorrent
|                     |                     | cpp-etherium

## Other Recent Packages 
In addition to the poll, each team member has packages they need for their own projects, so we work on those as well.  Here are some recent packages generated from that effort, which are done or almost done.  

* lz4 - compression 
* lzma - compression 
* mbedTLS - OpenSSL Alternative
* libevent - async programming
* libuv - async programming
* libwebsockets - websockets
* jsonformoderncpp - json
* libssh - ssh
* libiconv - char conversion
* libuuid - common lib for making uuid
* catch - unit testing
* cygwin_installer - windows posix shell
* caf - C++ actor framework
* giflib, libjpeg, libjpegturbo, libpng, libtiff, libwebp, libxpat
* glog/gflags - google libs

## Updates to Existing Packages
The packges for Abseil, Bazel, and Java saw some pretty major changes, and problems were fixed.  We are currently working on making the Bazel package build from source so that it covers more platforms.  We're also working on updates to Microsoft libraries including CPPRestSDK and the Azure IOTHub SDK for C (which includes the c libraries: uMQTT, uAMQP, and uHTTP). 


## Summary
In trying to write this blog post, I realized I couldn't even cover everything, so please keep an eye on our twitter, as check our Bintray feed directly: 

[https://bintray.com/bincrafters/notifications](https://bintray.com/bincrafters/notifications)


