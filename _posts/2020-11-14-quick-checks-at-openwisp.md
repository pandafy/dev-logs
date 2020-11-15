---
title: Quick checks at OpenWISP
published: true
---

Yesterday, I [opened the PR on ansible-openwisp2 to add default access
credentials](https://github.com/openwisp/ansible-openwisp2/pull/220) on a fresh
installation of OpenWISP. I requested a review from the other maintainer on
opening the PR and without realizing my implementation was a bit broken.
Hopefully, the maintainer realized it was still a work in progress and gave
constructive feedback to improve it. The improvements suggested by the
maintainer were very straightforward to implement. The tricky part was to fix
the entire implementation. I tried different ways to implement it. I discussed
those implementations on Ansible’s IRC channel.

After a brief discussion on IRC, I was able to implement it in a way that was
working and seemed pragmatic. An idempotence test was falling. I was unable to
find the reason for it. I called it a day and thought of asking other
maintainers how to get it resolved.

-------------

### In other news

Times are really confusing when I don’t have an assigned thing to do.
