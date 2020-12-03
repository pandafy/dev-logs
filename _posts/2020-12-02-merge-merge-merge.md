---
title: Merge! Merge! Merge!
published: true
---

After merging the patch to openwisp-controller, I proceeded to update my work
on ansible-openwisp2 yesterday. Things didn't go as planned and for some
reason, the build was stalling. I was astonished to learn that the default
timeout for a job on GitHub actions is 360 minutes. Honestly, 6 hours is a
lot of time and I believe that GitHub could be simply wasting their resources
by having that long timeout.

It was relatively easy to find the cause of stalling builds.
`openwisp-controller~=0.8.0` uses `channels~=2.2.0`. The task which installed
`channels_redis` did not pin the version, therefore it was installing the
latest version of `channels_redis` which was `~=3.2.0`. `channels_redis~=3.2.0`
increased the `channels` dependency to `channels~-3.0.0`. I assume that pip was
having troubles resolving the dependencies which stalled the build.

After fixing the stall, we were able to merge two PRs, one for
[substituting GitHub Actions for Travis CI](https://github.com/openwisp/ansible-openwisp2/pull/224)
and the other for [upgrading openwisp-controller dependency](https://github.com/openwisp/ansible-openwisp2/pull/206).

So much of our time is getting wasted because of Travis CI. Migration from one
CI service to another comes with its headaches. Many times, we face a problem
which was simply not there with Travis CI integration,

Ansible Galaxy has a hardcoded integration for Travis CI. I feel this a bit
stupid to just support only one CI service instead of having something
generalized. I saw a few issues created on their GitHub repository for this
and hope that someday they will make the integration CI neutral. For now, the
workaround is to use an ansible-galaxy command to import build information to
Ansible Galaxy.

I overlooked that GitHub Actions which are triggered by pull requests from
forks do not get secrets for their runtime. Due to this fact, the job
responsible for importing build details to Ansible Galaxy fails for a PR
created from a fork.

After fiddling with GitHub Actions, we concluded that we can still merge open
PRs and come back to this later on. We further merged two more PRs merged in
ansible-openwisp2, one for [static files minification and cache invalidation](https://github.com/openwisp/ansible-openwisp2/pull/222)
and the other for [introducing openwisp-notifications](https://github.com/openwisp/ansible-openwisp2/pull/215).

-----------------

### In other news

I was expected to work on BentoML today. I have an idea to achieve Kafka
integration. I hope the idea will be accepted by BentoML maintainers and
implementable by us.

