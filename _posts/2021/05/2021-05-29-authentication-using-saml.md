---
title: Authentication using SAML
---

Last week I worked on adding support for registration using SAML in
[openwisp-radius](https://github.com/openwisp/openwisp-radius/pull/262). It had
to look it up as I only heard about SAML and never worked with it. I found
multiple modules for adding SAML support to a Django project, out of them
`djangosaml2` stood out.

[`djangosaml2`](https://djangosaml2.readthedocs.io/) is being actively developed
and maintained. It uses [`pysaml2`](https://pysaml2.readthedocs.io/en/latest/)
which is also maintained by the same organization,
[`IdentityPython`](https://idpy.org/). This made me confident that I’ll be able
to get help if I got stuck. Later I came to know that IdentiyPython also have a
fairly active slack server.

OpenWISP required doing custom things that were not possible with `djangosaml2`
so I ended up sending a patch upstream. My patch was not merged, but it was
well-received. Later, the maintainer sent another patch that completed the
goals of my patch with other things.

I used Auth0 as an identity provider for my testing and it served me well.
Working with SAML was not a cakewalk. It took more time to configure
openwisp-radius for testing than to write code.

The code of `djangosaml2` got me interested. It is not very consistent and
needs some improvements and I think this is the area where I can help. I will
try to keep contributing to djangosaml2 and help another opensource project.
