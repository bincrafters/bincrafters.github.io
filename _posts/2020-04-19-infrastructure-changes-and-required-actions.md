---
layout: post
title: Infrastructure Changes and Required Actions
tags: [Conan.io, infrastructure, artifactory, bintray, remote]
---

We have some important changes in our infrastructure. Consumers of our packages need to perform some manual steps in order to continue using our packages beyond May 1, 2021.

---

Since the beginning of Bincrafters, our packages are hosted on Bintray. In February, JFrog [announced the sunset of Bintray](https://blog.conan.io/2021/02/05/JFrog-announces-sunset-bintray.html) (see also [this Conan blog post](https://blog.conan.io/2021/02/05/JFrog-announces-sunset-bintray.html)). On **May 1, 2021**, [Bintray will shut down forever](https://blog.conan.io/2021/03/31/Bintray-sunset-timeline.html) and with it our current Conan repository at `https://api.bintray.com/conan/bincrafters/public-conan`.

JFrog offers [Artifactory](https://jfrog.com/artifactory/) as one possibility to host a Conan repository. In addition to the opportunity to install Artifactory on own servers, they also offer managed Artifactory cloud instances which also includes a free trier.

Since we build and provide binary packages for a huge amount of configurations, we always required a lot of space and network traffic. JFrog generously sponsored us by effectively making our Bintray account unlimited and helping us to cover costs for CI.

We are thankful that JFrog decided to continue to sponsor us, even after the sunset of Bintray. We now have a sponsored Artifactory instance at [bincrafters.jfrog.io](https://bincrafters.jfrog.io).


## Required Actions - What you need to do

In order to continue to consume Bincrafters packages, you need to change our remote URL from pointing to Bintray to our new Artifactory instance.

If you have named our remote `bincrafters`, you can execute the following command to update our remote:

> $ conan remote update bincrafters https://bincrafters.jfrog.io/artifactory/api/conan/public-conan


Additionally, this new remote requires Conan clients to have revisions enabled. This was not the case with our Bintray remote.

If you have not enabled revisions yet, you can do so by executing

> $ conan config set general.revisions_enabled=1


You can start using our new remote right now. We recommend switching to the new remote as soon as possible, to have enough time to solve potential unwanted side effects of these changes.


## Breaking Changes

Our new remote should still offer all recipes and binary packages that you would get from our Bintray remote up to May 1, 2021. This is due to the fact, that our Artifactory remote integrates the Bintray remote transparently.

We made the decision to copy all _**recipes**_ from our Bintray remote to Artifactory, but not the _**binary packages**_. This means, that after the 1st of May, our Artifactory remote will not provide _**old binary packages**_ anymore that previously existed.

One reason for this decision was the fact that many of the recipes and their binary packages got obsolete in the meantime and, for example, can now be found directly in the [Conan Center Index](https://github.com/conan-io/conan-center-index). When it is possible, we migrate our recipes there and welcome help from contributors for such migrations.

The other major reason is the enormous size of all binary packages combined, which we would need to transfer and verify. The disadvantages of having these packages around further might easily outnumber the advantages.

_**For new recipes and recipes revisions we continue to build and provide binary packages via our new Artifactory remote.**_

In a nutshell, on May 1, 2021 the vast majority of currently existing binary packages will not be available anymore, but all recipes should continue to be available from our new Conan remote. If you notice missing recipes or similar unexpected behaviour, please reach out to us.

We recommend to not expect that our remote offers binary packages for a specific  configuration. Instead, set a [build mode](https://docs.conan.io/en/latest/mastering/policies.html) like `missing` (or `outdated`) in order to tell your Conan client to build the packages if they are not available.

---

If you notice missing recipes, other unexpected behaviour, run into problems or have questions regarding these changes, please either [open an issue on GitHub](https://github.com/bincrafters/community) or [reach out to us in Slack](https://app.slack.com/client/T21Q22G66/C77T8CBFB).
