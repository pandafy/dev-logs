---
title: Tests in OpenWISP
---

I was reading about Software Testing while preparing for my university exams.
When I wrote tests for OpenWISP Notifications, I barely knew any concepts of
software testing. I didn’t read anything about how to write tests. I had the
sole goal of attaining 100% coverage and try all possible scenarios.

Now when I read about testing methodologies and tests, I can relate to why the
tests were written like that.

I came across the concepts of `driver` and `stub` under the topic of Unit
Testing. Unit tests are written for individual modules and it might be possible
those individual modules are not able to run on their own. For testing,
additional code is added to run individual modules.

`Driver` is the piece of code that allows the execution of the current module
for the purpose of testing. `Stub` is the code that allows the execution of
multiple modules together.

I might be wrong here, but I believe there is a very thin line for
differentiating drivers and stubs in the test suite of OpenWISP Notifications.
The test project works as both the `stub` integrating `openwisp-utils` and
`openwisp-users` and the `driver` by providing run-time for the execution of
tests of `openwisp-notifications`.

-----------------

### In other news

A design oversight is coming back to haunt me in OpenWISP. To delete obsolete
notifications, a task is run for every `pre_delete` signal dispatched. This is
flooding the celery queue for tasks for irrelevant objects and storming database
queries. A discussion for an optimal solution for this problem is going on at
[openwisp/openwisp-notifications#163](https://github.com/openwisp/openwisp-notifications/issues/163).
