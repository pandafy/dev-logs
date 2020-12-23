---
title: Agitation, not the bug
published: true
---

There are two potential release blockers for ansible-openwisp2. Since these bugs
arose due to changes that I made earlier to the repository, as a pragmatic
programmer I am taking up the responsibility for my code and fixing it.

Today, I primarily focused on [finding the bug that broke the leaflet marker
icons](https://github.com/openwisp/ansible-openwisp2/issues/232)
and then hopefully fixed it. The issue description suspected that the
static file cache invalidation broke the feature.

I was relieved that the bug was easy to replicate. I replicated it in the test
project of openwisp-controller. This made working on the fix quicker than it
would have been possible on a remote machine.

From the file names in the network tab of web developer tools, I suspected that
static file cache invalidation was not the direct cause of this. It agitated
the bug, but it was not the cause. It has to be something in Javascript.


Using information from the initiator tab of the missing resource, I tracked
down the JavaScript code which was responsible for rendering the icons. After
setting up multiple breakpoints and following the call stack I was able to find
the cause of the bug.

The bug lies in the Leaflet JS library itself. The library extract location of
the icons through [string manipulation using regex](https://github.com/Leaflet/Leaflet/pull/7092/files#diff-65510978f847aaaf9307d30495332de39ecfed44ec25372d1338456e7d953a17L51-R62).
Since it is hard-coded for the image names that are shipped with the library,
the regex breaks for filenames containing hash(cache invalidation mechanism). A
[PR was already open](https://github.com/Leaflet/Leaflet/pull/7092)
to fix it. Till the PR is merged in the leaflet, we will have to create a
workaround in OpenWISP. It was suggested by the maintainer to create a custom
static storage class that excludes leaflet static files from the cache
invalidation mechanism.
