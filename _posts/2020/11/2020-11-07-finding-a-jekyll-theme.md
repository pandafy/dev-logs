---
title: I spy through my eyes, a Jekyll theme for my blog
published: true
---

**Note:** This dev log got lost in Git shenanigans. Another writeup is under progress.

-------------

### In other news

I asked a few of my queries on Ansible’s IRC regarding idempotence test failing
for installing openwisp modules through URL in ansible-openwisp2.
I was told that “pip is not very introspective”.
The pip module of Ansible is a thin layer around the actual pip package.
Pip installs packages from a link everytime it is run, therefore making a change
even if the package is already installed. I decided to skip the idempotence test
for the task concerning installing python packages from URLs.
