---
layout: post
title: 'Bincrafters Shoutouts'
tags: [Conan.io, Bintray]
---

The Bincrafters team recently hit double digits, which feels like a big accomplishment for us.  Each member has brought a unique combination of experience, insight, and Conan recipe's to the table.  This has allowed us to start checking multiple packages off our list each week for the last two months.  It's also allowed us to level-up our packaging game in a few cases. This post is just to highlight how valuable and appreciated everyone's time is, before we start on a next trial of strength... packaging Qt. 

---
## Boost and ICU

During the process of packaging Boost and ICU, it was truly remarkable how much time the early members invested. It took just over 3 months to really get it right, and several members of the team worked for what had to be 20+ hours each week during that time.  Again, I highlight @grafikrobot who was the wizard-tank who slogged through the hardest parts of this.  However, major time investments and contributions were also made by @SSE4, @sigmoidal, and @uilianries during this period.  Had these members not come aboard when they did, we would NOT have finished before CPPCon, or potentially at all honestly.  

The reason it was so challenging is that rabbithole after rabbithole kept cropping up and demanding to be explored, and thus we kept discovering nuances which often caused us to refactor major components (mostly the Boost.Generator, and Boost.Build packages).  Conan is a very powerful and flexible packaging system, and B2 is a very powerful and flexible build system, and we needed to bring all their power to bear in order to make these packages work.  Also, as many readers already know, Boost and ICU just happen to be complex on their own. So, automating cross-compilation and interop between them was a devops obstacle course.  We even needed to request and submit PR's for modifications and extensions to Conan features, which the Conan team swiftly addressed.  

## Other Challenging Libraries

During and since Boost and ICU, we've continued to wrestle with other libraries as well.  The Microsoft libraries we've packaged are somewhat challenging, and have several of dependencies like Boost and OpenSSL.  Since we setup CI to build cross-platform on all our packages, the challenges get multiplied x3.  So, again I want to highlight the contributions of @ulianries and @SSE4 for taking the leads on multiple complex and sometimes frustrating packages while Boost and ICU were under construction.  

## New Members

In the past two months, several community Conan members have decided to join our team and bring their high-quality pre-existing packages with them. They no doubt spent a great deal of time learning Conan, and creating and troubleshooting these packages on their own. Rather than list them all here, you can see our active member list here: https://bincrafters.github.io/about/ .  We have tremendous appreciation for them as well. 

## Thankless and Anonymous

In the world of Open-Source software, packagers are perhaps the least-recognized members of the community, which might be surprising to some since devops tends to be some of the most frustrating work in software.  There are vast numbers of people who have been doing the difficult work of packaging for all the linux distros for decades. We are standing on the shoulders of these giants, yet they are effectively anonymous to most of us, despite deserving a lot of credit and gratitude. The same is now becoming true for the Homebrew and Chocolatey teams now, as they try to package for their respective operating systems, and so the same is true for the Conan community.  Of course, a library which we might spend a few days or a month packaging, one or more library authors might have spent several years creating and evolving, so we recognize and appreciate them as well.  OSS truly is an ecosystem with many critical parts. 

## Summary

The rest of the Conan user community has been great in terms of making Bincrafters feel recognized for their work and encouraging us to continue, both on Twitter and in Slack. These things might seem insignificant to some, but it really does help some of us feel like we're making a difference.  So, we also want to say thanks to those folks for the feedback.  And, finally, we must say thanks once more to the team at Conan.io once again for creating such a special platform for us to build upon, and Bintray for backing it up with best generic binary hosting service the OSS community has ever had. 


