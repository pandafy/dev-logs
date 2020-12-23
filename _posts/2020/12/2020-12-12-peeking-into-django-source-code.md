---
title: Peeking into Django’s source code
published: true
---

I picked up [another small issue on Kiwi TCMS](https://github.com/kiwitcms/Kiwi/issues/1605).
This one is for writing tests for their custom Middleware. Initially, I
chose to use actual GET/POST requests and test the working of the
middlewares, but I changed my mind later after taking account of tests I
wrote for `SafeJSONRPCHandler`.

I looked up Django's source code to learn how they have written tests for
their Middlewares. They had used `HttpRequest` objects to mimic an actual
request. Then, they asserted on different attributes of the request object
to verify that their middlewares are properly working.

Taking inspiration from Django’s tests, I also mimicked the request object
and asserted on attributes of the request objects which were expected to be
modified.

-----------------

### In other news

BentoML maintainers asked us to schedule another meeting with them to discuss more about the Kafka Integration. As this is the last week of the Fellowship, I don’t have high hopes for getting it to complete the PR in the tenure of the Fellowship.

I opened a [small PR in the openwisp-controller for adding a note](https://github.com/openwisp/openwisp-controller/pull/349).
It was about a feature I added in ansible-openwisp2 that automatically
creates a default access credential and default template to configure
`authorized_keys` of network devices. The feature made a part of
documentation obsolete for users who used ansible-openwisp2 for installing
OpenWISP.
