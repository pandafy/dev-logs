---
title: Scrutinizing OpenWISP Controller 0.8.0
published: true
---

I added GitHub Workflow for continuous testing on ansible-openwisp2 yesterday.
The failing build suspected something is wrong in the latest release of the
openwisp-controller.

The test suite for the master branch of openwisp-controller was failing locally
with a random error. I suspected that maintainers will release the module with
a failing test suite. It had to be something in my development environment.

OpenWISP’s account was still out of TravisCI credits. So I wrote another GitHub
workflow for the openwisp-controller. This was dead easy. I just copied the
whole YAML from openwisp-controller, made a few tweaks and it started working
fine. And yes, the build was passing on GitHub Actions and my suspicion was
right, my development environment was outdated.

After making sure that the test suite for openwisp-controller was passing for
the master branch, I began to dig into the code. Quickly, I saw the problem.
An openwisp-controller setting was directly used from the Django’s setting
object instead of from the module’s settings. I thought changing that will fix
everything. After making those changes, the build for openwisp-controller was
passing but ansible-openwisp2 was failing.

This bug was more complex than I thought. After banging my head on the
codebase, I figured out that the cause of this problem was in `settings.py`.
A setting was set in the test project of openwisp-controller which was missing
in ansible-openwisp2. I removed that setting from the `settings.py` and mocked
it for the test cases which relied on it.

Again, the test suite was passing for openwisp-controller and failing for
ansible-openwisp2. But, I have made progress at this point. The number of
failing tests reduced.

The remaining test cases which were failing complained that a mocked function
was never called. I was completely clueless about this error. I asked for help
on the OpenWISP Gitter channel and called off the day hoping that someone
could help me with this.

-----------------

### In other news

An OpenWISP user was having trouble upgrading the openwisp-controller to 0.8.0
with the current ansible-openwisp2 role. I felt bad that due to me, users are
not able to use the latest release of OpenWISP which is packed with so many
goodies. This made me more desperate to completely fix these issues and get
it working.
