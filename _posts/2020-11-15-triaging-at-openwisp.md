---
title: Triaging at OpenWISP
published: true
---

I went through all opened PRs on OpenWISP trying to add them to the respective
project boards. Organizing PRs on the project board is important because only
then we can ensure that the time spent by the maintainer are well utilized and
PRs which need review get reviewed.

While going through these PRs, I reviewed some which were not already reviewed
by someone. I added comments in others and added labels on those which seemed
appropriate.

I fixed the idempotence tests which was failing in my
[PR](https://github.com/openwisp/ansible-openwisp2/pull/220) yesterday.
The community at Absible’s IRC is great. Now, I don’t feel like I am only on my
one. I know that if I can't find an answer to my problem, someone has my back
to solve the issues I run into.

I opened another [PR on ansible-openwisp2 today for adding support for the
openwisp-firmware upgrader](https://github.com/openwisp/ansible-openwisp2/pull/221).
I thought that doing this PR would be a pain but it was relatively easy.
Dependencies gave me a headache. I also ended up creating a
[PR to openwisp-firmware-upgrader to refactor the URL routing](https://github.com/openwisp/openwisp-firmware-upgrader/pull/109).
With this PR, it will become easy for users to add the
openwisp-firmware-upgrader module in their project.

-------------

### In other news

As a part of the MLH Fellowship, we have a hackathon dubbed
“Mid-way hackathon” incoming. In this hackathon, teams can be made across the
pod. I was too occupied in the previous week to care about this hackathon. I
didn’t read the emails, I didn’t think of any project ideas, I didn’t post a
pitch for joining other teams as free agents. In short, I was lazy and
uninterested. I was at a point where I was thinking if there is a way to
willingly opt-out of participating in this hackathon and continue with the
weekly routine. Then came a few of my podmates to save me. They asked whether I
would join their team and I hopped in without thinking twice. I tried to save
myself from thinking out a project idea on my own or pitching myself to others
so they recruit me. Anyway, I like the team I am part of, they are all smart
and accountable people who are willing to win the hackathon.
