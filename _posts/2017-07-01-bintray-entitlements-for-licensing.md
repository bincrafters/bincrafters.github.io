---
layout: post
title: 'Bintray Entitlements - A Modern Way to Profit on Code'
tags: [Bintray]
---

If you make modern applications or software libraries and are having difficulty with the "profit" part, the Bintray entitlements system might be able to help you. 

---

## How it Works
Bintray entitlements are a mechanism to control customer access to private repositories.  Rather than a traditional approach where a user or machine's right to a piece of software is validated "on-use" by virtue of a license-key activation strategy, entitlements validate a user or machine's right to a piece of software "on-download".  This is not a new idea in itself.  What is new with Bintray and the "Entitlements" system, is that it provides an integrated hosting and licensing platform, so that software vendors and individual developers don't have to re-invent this part of the delivery pipeline. 

One important thing to note here is the emphasis of this feature for **Modern** applications and libraries.  This is because Bintray entitlements controls how people download your software.  If you are frequently releasing updates and customers benefit significantly with every passing release, then it makes much more business sense for them to keeping an active license or subscription with you.  If the user cancels or fails to pay, you can deactivate their entitlement, and they can no longer download.  This is the type of software licensing and delivery model for which Bintray really shines.  Of course, Entitlements it still work if you release software less often, but then the liklihood of piracy or circumvention of your licensing strategy goes up. 

## What it Provides
### Hosting
If you're familiar with Bintray's hosting system, you can skip this section.  Otherwise, Bintray allows users to create unlimited repositories for hosting files, with a focus on software packages. For example, to host Java packages users can create Maven repositories, to host .NET packages users can create Nuget repositories, for C++ it has Conan repositories.  There's also a "generic" repository type that can hold any file type, such as `.zip` or `.tar.gz` files for distributing source code. [The complete list of repository types](https://bintray.com/docs/usermanual/formats/formats_supportedpackageformats.html) can be found here.  

### Access-Keys
The fundamental unit of "authentication" with the Bintray entitlements feature is an "Access Key", which is effectively a username and password pair.  It also features the ability to whitelist and blacklist access based on Source IP address, and the ability to auto-expire keys.  So, there's a set of APIs for provisioning and managing access keys. 

### Entitlements
The fundamental unit of "authorization" with the Bintray entitlements feature is an "Entitlement", which effectively grants one or more keys permission to download one or more files and directories.  

### User Experience
One thing that is very exciting about Bintray Access Keys is how users can actually use them.  First, the can be used on the Bintray website to browse your published files and see those which they have access to.  However, the really cool part is that they can be used as credentials in the package management clients for the corresponding repository type.  So, for the examples repositories listed earlier, they can be used in Maven clients, Nuget clients, Conan clients, etc. 

### Extra Features
Because it's a cloud-based platform designed for scale, Bintray has implemented a number of core features such as "tagging" for these entitlements which feed into a "statistic and usage reports" system.  It also has thresholds, binary signing,  

## What you Still Need
### A User Interface
While Entitlements can be a backend for your software delivery pipeline, it's not a front end.  You'll still need to have a separate customer-facing web portal.  

### Billing
Licensing != Billing.  Bintray's Entitlement API provides the mechanism to control users and access, but does not help you collect money.  There are many cloud providers which offer secure billing-as-a-service with robust APIs, so it's generally best to integrate with one of them rather than writing your own code to collect payment. 

## Other Uses for Entitlements - Internal Access Control
While this article focuses on using entitlements for profit, objectively speaking it is simply an access-control system.  Thus, there's an entirely separate use case for it when it comes to large software development teams and companies which need the ability to automate access to their software for their staff and contractors.  With developers often joining and leaving companies and projects, VPN-based solutions struggle to be effective, so controlling access via a cloud platform like Bintray can be a huge win. 