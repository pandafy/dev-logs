---
title: Managing dependencies
published: true
---

I did not code much today but it was certainly not a no-code day. I reviewed
some PRs on OpenWISP and helped follow contributors with their blockers.

A new bug surfaced in ansible-openwisp2 that made the builds fail. It was very
certain that this bug is due to some dependency issue. A quick web search did
not reveal anything, so I gave the traceback a deeper look.

The error traceback pointed towards the `pyopenssl` and `cryptography` modules.
I suspected that a new release from any of these modules could be responsible
for the error. I checked the changelog of both the modules and voila, there
was a new point release of cryptography that was issued just yesterday.

There were several backward-incompatible changes mentioned in the release notes
of `cryptography 3.3` but none of them mentioned anything regarding the errors
we were facing. This is the main reason I strive myself to write better
release notes every time.

I had to dig deeper to find my answers and I needed answers. I spun up a
machine on the cloud and used the ansible-openwisp2 role to install OpenWISP on
it. The playbook errored out in the middle, just like the builds. But unlike
the builds, I have an environment I could play with.

I checked the installed versions of the problematic modules and indeed
`cryptography 3.3` was installed along with `pyopenssl 19.0.0`. I upgraded the
`pyopenssl` to the latest version and the bug disappeared like a charm.

I concluded that `cryptography 3.3` is incompatible with 19.0.0. After playing
with different versions of these modules I figured out `cryptography 3.3` is
compatible with pyopenssl 19.1.0. But the strange thing is that `pip` should be
able to install this version of `pyopenssl` since `django_x509` has pinned
pyopenssl to `<20.0.0`.

I installed `pipdeptree` on the remote machine to get the dependency graph of
the virtual environment. After reading lots of changelogs and trying to
troubleshoot the dependency conflicts, I gave up. I could not pinpoint the bug.
I was able to just narrow down the cause. I [shared my findings with the
maintainers](https://github.com/openwisp/ansible-openwisp2/pull/223#issuecomment-741607991)
with the hope that they will be able to build upon my work and find the real
cause.

I also updated my PR on ansible-openwisp2 to fix broken leaflet markers. I
forgot to add a file that was responsible to use the custom storage class that
I wrote.

-----------------

### In other news

I thought waiting for a response from BentoML maintainers will do me no good,
so [claimed a small issue in Kiwi TCMS](https://github.com/kiwitcms/Kiwi/issues/1611).
It looked easy in the beginning but I got stuck with it for a week now. I asked
the maintainers to help me out with it and told them possible ways to solve the
issue.

I caught up with the GitHub Universe event today. It was all about DevOps today
so learned a lot about GitHub Actions and enjoyed everything I watched.
