---
title: Pip gone rogue
published: true
---

Pip has rolled out its new dependency resolver algorithm in `20.3`. The new
dependency resolver algorithm has caused numerous problems across the Python
community. OpenWISP has also become a victim of a bug in the new dependency
resolver algorithm.

The new dependency algorithm sometimes stalls while resolving dependencies or
gets stuck in an infinite loop.

We faced this problem for the first time in ansible-openwisp2, where the task
responsible for installing openwisp-controller stalled. We were unsure of the
reason. We implemented a workaround by pinning down dependencies and
miraculously that prevented the said task from stalling.

We found another occurrence of this bug in a [build log of openwisp-monitoring](https://travis-ci.com/github/openwisp/openwisp-monitoring/jobs/457198892#L500)
yesterday. Since, this time the logs were in front of our eyes and not
cluttered with the formatting of Ansible, it was easy to figure out what was
happening.

From an initial inspection, it looked like pip was having a hard time
resolving the dependency of django-celery-mail. I created a new virtual
environment and started playing with different versions of dependencies to
figure out a fix.

It turns out the [django-celery-email](https://github.com/pmclanahan/django-celery-email)
has not pinned an upper version limit for celery. django-celery-email was
trying to install `celery~=5.0` while the openwisp-controller has pinned it at
`celery~=4.4`. This was making the new dependency resolver to freak out.

Removing django-celery-email from the requirements of openwisp-monitoring
removed this conflict and pip was able to peacefully install
openwisp-monitoring. Also, django-celery-email is a module that is used in
production environments. And, it is expected from the developer to know about
it and update the email backend in production. I [opened a PR in openwisp-monitoring](https://github.com/openwisp/openwisp-monitoring/pull/254)
making this change.

I created a meme for this behavior of pip because I couldn't help myself.

I also updated my PR for introducing GitHub Actions for CI in openwisp-radius.
The PR lost its priority earlier since Travis started working again and there
were more important things to solve in other OpenWISP modules.

-----------------

### In other news

I helped some OpenWISP community members to install openwisp-firmware-upgrader
on a production instance. I was able to pinpoint the exact cause of their
problem without knowing the complete description. By contributing to
ansible-openwisp2 in the past, I am familiarized with some gotchas. It felt
like a *pro* debugging their problems.
