---
title: Finishing the job
published: true
---

Adding support for openwisp-controller 0.8.0 in ansible-openwisp2 has become a nightmare for me. There are so many PRs that are dependent on this and so many bugs are popping up one after another. This is pissing me off now.

While going through `settings.py` of openwisp-controller yesterday, I forgot to notice that there was another set that was set for running the test suite. Like earlier, I "yeeted" the setting and mocked it for tests that relied on it.

And guess what, the build for openwisp-controller was passing but failing for ansible-openwisp2. But again. I have made some progress and reduced the number of failing test cases. I was relieved that at least I was on the right track.

It occurred to me that this is the best I could do with my instincts, I had to make my hands dirty to progress ahead. I spun up a machine on AWS and used the ansible-openwisp2 role to install everything on it.

I pinpointed the code which was responsible for the falling tests. I used the ever so trustworthy print statements to understand what is happening. I realized that these tests were asynchronously calling a celery task. In all of OpenWISP's projects, we set celery on eager mode while running the test suite. This was the missing link, the root of all evil. I added the missing link and voila it worked.

-----------------

### In other news

I have to give a talk about GSoC to a student community. I was supposed to create slides for it today. Honestly, talking about GSoC has become a cliche for me. It does not excite me anymore. I just hope it goes well.
