---
title: No Code Day - Failed
published: true
---

I have been told that I spend too much time sitting on the computer and I
should do other things than computers. So, today I decided to take a break
from code.

It was all going well, until around midnight I received an email notification
that openwisp-firmware-upgrader has been released. The release of this module
has been stalling my work for over a week now. I got excited and ditched No
Code Day for good. In my defense, I didn’t code a single line during the day.

So I went back to the keyboard and started updating my PR on ansible-openwisp2.
Sadly, TravisCI credits for OpenWISP’s account were all consumed. I thought it
might be a good idea to write a GitHub workflow for continuous testing in
ansible-openwisp2.

From my previous experience with GitHub Actions, I expected the process to be
quick. I read a few blog posts and watched some tutorials for writing a GitHub
workflow to test an Ansible role with the molecule module.

It all went well. My previous attempt at writing a GitHub workflow for
openwisp-notifications helped a lot. I copy-pasted from here and there and
voila, the workflow was complete. I tested it on my fork first. As expected,
it failed for the first build. After lots of tweaking, setting up environment
variables, and referring back to the `travis.yml` a couple of times, I finally
got it working.

Now, with the GitHub Actions working, I was relieved that we can be sure to
merge these PRs. I ran the build for my PR, and it failed. From an initial
look, I suspected it is something related to openwisp-controller 0.8.0.

I was not ready to jump into a rabbit hole at this time. I called off the
day(or night). Let’s see what is in the openwisp-controller tomorrow.

-----------------

### In other news

I should really find hobbies other than computers.
