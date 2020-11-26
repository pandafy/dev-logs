---
title: Aha! Minor Project
published: true
---

I have not paid any attention to my minor project for a month now.
As the mid-term evaluation is approaching, the pending work is
getting to my nerves.

I decided that I will create a progress report for the minor project today.
Creating the report would have been easy if there were a project to track the
progress of. So today, I not only have to create a progress report but also to
create a project itself.

Thankfully one of the team members found some project on GitHub which did some
part of what we were trying to achieve. We are supposed to develop a TTS
application for the Sanskrit language.

A huge shoutout to Sanskrit Open Source Programmers
for aggregating a plethora of helpful resources for developing a Sanskrit TTS
application. Due to them, we have found an audio corpus, a text corpus,
and a community of developers and researchers who are working in the same field.

The only thing which lacks in their projects is documentation. Their projects
are scarcely documented. I had to use my Python programming instincts to make
them work. It is due to those instincts, I spent over an hour wondering why the
modules are not getting installed.

I used `pip install .` instead of `pip install -e .`, notice the `-e` flag.
The `-e` flag installs the project in editable mode, which means I can modify
the code without worrying about installing the updated code.

By the middle of the night, we completed our progress report and hoped that
our mentor will be easy on us tomorrow.

-----------------

### In other news

My work in OpenWISP is still pending. Yesterday, I asked other maintainers
whether I can take over the work of another contributor that is stalling my
work. I have received a green signal for doing that. So tomorrow, I will try
to add support of openwisp-controller 0.8.0 to ansible-openwisp2 and will
complete my pending PRs after that.

