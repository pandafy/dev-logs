---
title: Slow and steady
published: true
---

Opened a [PR on ansible-openwisp2 to fix the leaflet map](https://github.com/openwisp/ansible-openwisp2/pull/238).
I tracked down the cause of this bug yesterday. My PR monkey patches the bug to prevent the release from further stalling. I [opened an issue in openwisp-utils](https://github.com/openwisp/openwisp-utils/issues/166) to implement this fix cleanly.

In [my PR to ansible-openwisp2](https://github.com/openwisp/ansible-openwisp2/pull/238),
I have implemented a custom storage class that inherits from the
`CompressStaticFilesStorage` class of the `django-compress-staticfiles` module.
The custom storage class adds an option to exclude certain files based on Unix
shell-style wildcards.


I already knew about the `re` module of Python which is used while working with
regular expressions. But today, I came across the `fnmatch` module. The
`fnmatch` allows matching a string based on Unix shell-style wildcards which
are way easier to use than regex. These wildcards are perfect for use in this
PR since it matches the file name and using `leaflet/*/*.png` matches all PNG
files of the leaflet module.


Apart from this, I reviewed some work from other contributors.

-----------------

### In other news

I was under the assumption that GitHub Universe will start from tomorrow.
Even a banner on their website was stating that the events will start in 10 hours. I saw a lot of people tweeting about new features. I started wondering why GitHub
is releasing these features before the event. Thanks to my friends who made me
aware that the event has started today for America/Europe region and they have
a different schedule for the Asia/Pacific region.
