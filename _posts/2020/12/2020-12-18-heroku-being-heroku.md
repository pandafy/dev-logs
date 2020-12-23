---
title: Heroku being Heroku
published: true
---

Yesterday, I completed developing the web application for ShrutiVaani -
Sanskrit TTS. I deployed an initial version of it on Heroku to make sure that
at least the Django part works fine on the cloud.

I also connected the web application to the runtime of our TTS application. The
whole application was working fine locally. Today, I aimed to upload the TTS
runtime to Heroku as well.

This would have been an easy job, but the modules which we were using for
creating our TTS application were not correctly packaged. Luckily, the source
code of all of the packages was organized under the same organization on
GitHub.

I had to fork those packages and fix them to be able to install them on the
Heroku instance. They had made several silly mistakes like not following their
own conventions. So, instead of installing those modules from PyPI, I was
installing it from my fork on GitHub which is not really an issue.

After preparing the `requirements.txt`, I pushed all the changes to Heroku.
Then Heroku being Heroku, started to throw errors while building some python
packages. Apparently, many C libraries were not available on the Heroku
instance which were required by these Python packages.

Using the `Aptfile`, I added the required system packages to be installed
before installing the Python packages. And, it still didn’t work as expected.

I will try to make it work tomorrow by any means. Maybe, I should have started
by creating a `Dockerfile` from the beginning.

-----------------

### In other news

Solved a few MLH Fellowship CTF challenges today. I again got stuck on one,
then didn’t continue.
