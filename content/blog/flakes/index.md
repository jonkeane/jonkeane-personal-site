---
title: There is no such thing as a flaky test 
date: 2024-03-10
cover_image: _DSC2699.jpg
slug: flakes
---

"Is that failure a flaky test? — We can ignore that failure, it's a flake — Let me rerun these — that's a flake." everywhere that I've worked; every team I've worked with I've heard these or similar[^1]. When I was earlier in my career this felt reassuring and calming. The test failed, but it's ok! It sometimes just does that, click re-run and move on. Simple! But it also left me unsatisfied: I couldn't ever stop that nagging voice in my head from asking "but why?". Which ultimately brought me to the conclusion that there is no such thing as flaky tests.  

I can hear the shouts on the internet already: "No, no this test really does only fail sometimes. That's the definition of flaky!" and that is absolutely true, that is the definition of flaky. But a test that fails sometimes is not a test that we should rely on. A test that fails sometimes leads us to either reflexively re-run tests when we see a failure or worse, become desensitized to seeing red in our testing and ignoring it. And in that way, a test that fails sometimes is worse than no test at all!

### Ways tests go bad

So if there is no such thing as a flaky test — what is going on here? Why do people call tests flaky? Ultimately, I've found that so-called flaky tests are ultimately tests that have been poorly designed or implemented in some way. And the great thing about this framing is that it gives us something that we can improve when we stumble on a test that isn't helping us the way it should. I'll go over some of the common ways that tests can be poorly designed or implemented that make them go bad — but this list is not exhaustive. And which of these that apply to you will vary based on what you're building and testing.


#### testing at the wrong level

The more layers you have in your tests, the more things to go wrong. MOCKS!

#### testing code that is poorly structured

Poorly structured code makes it difficult to test encapsulated behaviors. This can lead to testing at the wrong level.

#### randomness

You probably don't need randomness, but if you do be sure you characterize it in your tests + they can handle if they find themselves to be problematic.

#### configuration

This is one of the most straightforward to identify and also one of the ones that can take a lot of work and knowledge to get right. All test environments need to be bootstrapped and setup things like the test running framework, installing dependencies, etc. If something goes wrong in this process the whole run looks like it failed. This is typically easy to identify in your test logs[^2]. Some of these are inevitable. If the dependency repository you're using to install goes down, there's not much you can do about that. But each time you see something like this you can ask yourself: how common is this? If it's happening frequently enough that you notice a pattern, maybe you should consider using a different mirror or change the approach you have for dependency resolution. 

One example that I ran into recently working on the [Apache Arrow](https://arrow.apache.org) extended CI, I noticed that some of our tests were failing due to dependency version mismatches in Debian's unstable versus testing repositories. We were using an image that happened to install a number of the core dependencies using unstable, but then our CI setup installed other dependencies with default arguments which in this case select testing. There was a version mismatch between two dependencies we needed to install, so the jobs failed. This particular mismatch likely would only last a few days or weeks as versions transitioned from unstable to testing — but it also showed that our original assumptions about the stability of the image we were using wasn't what we thought it was. We had assumed it was a more-or-less generic stable image, but looking at the documentation + a chat with one of the maintainers clarified it's actually much more of a bleeding-edge kind of image. For these particular tests, we didn't want or need the bleeding-edge[^3] for this, so swapping to an image that didn't have version mismatches like this meant these jobs were much more likely to only fail when we've broken something, not when there is a slight change in unstable versus testing dependency repositories. GitHub [issue](https://github.com/apache/arrow/issues/40323), [pull request](https://github.com/apache/arrow/pull/40321)


### So what should I do when someone says the test is flaky?

Use it as an opportunity to ask: Are these tests structured correctly? Are they testing the right layer? Are they testing code that is well encapsulated? Are they testing properties that are interesting, but not critical to the test? Is my testing setup and configuration problematic? The answer to some of these might be negative, and this is an opportunity to fix that. 


[^1]: Ok, this is actually a lie. I never heard this at places that eschewed testing entirely. Which—fair enough—I guess one way to never have failing tests is to never test anything. But that's a whole separate blog post.

[^2]: And if it's not — that is something you should absolutely change or reconsider your design!

[^3]: We *do* want and need to test against bleeding edge images, but those are separate tests that are targeted at that specifically. Those tests also use dependency resolution methods that are more amenable to changes like this. 