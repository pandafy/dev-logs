---
title: Clearing up my mess
published: true
---


It was pointed out in the review that I have not configured private storage
correctly in the PR for adding openwisp-firmware-upgrader support. I messed
up, I didn’t test my work properly.

It occurred to me that I never ran tests for openwisp-firmware-upgrader in the
verification task. If I had run it, the test suite would have failed and
pointed me to my mistake. It was a good opportunity to update the verification
task.

Updating the verification task should be straight forward, just write the name
of the test class, and voila. At least this is what I believed before jumping
in. After updating the verification task, the test suite started to fail. It
was complaining about some dependencies which openwisp does not package with
its module but is available in the development. I added a handy task to install
those dependencies. But even after that, the test suite failed.

A work of two minutes(updating settings) stretched over two hours. I was trying
to understand what is happening but failed at every attempt. At last, I had to
give up on updating the verification task and resort to the bare minimum of
updating settings and manually testing my work.

During this process, I found a problem with ansible-openwisp2. There is no
provision for a python virtual environment just for testing. Maybe in the
future, we could add it and be able to run more tests.

-----------------

### In other news

Finally, I could take out some time to work on BentoML’s Kafka integration. We
have finally figured out a place where the integration will fit in. We are
waiting for approval from the maintainers regarding the design.
