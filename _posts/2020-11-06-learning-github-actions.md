---
title: Learning GitHub Actions
published: true
---

Yesterday, I got frustrated with the slowness of Travis CI while working on OpenWISP Notifications.
Conversations with other contributors also suggested moving away from Travis CI for good.
Someone suggested using GitHub Actions instead of Travis to keep everything integrated in
GitHub itself. I decided to try out GitHub actions for OpenWISP Notifications to explore and
propose this change to be carried out in all of OpenWISP's repositories.

There were few gotchas while porting CI from Travis to GitHub Actions. The first thorn in the way
was the **checkout action** which creates a merge request in the local repository while running
the action. This was making QA checks to fail since OpenWISP's QA checks also check the
commit message.
I spent almost an hour looking for a solution on Google and StackOverflow but could
not find anything which worked for me. At last, I thought of checking out the code of this action.
At first, I went through the README, and viola, there was my answer. I guess, the developers of the
action already knew about such a use case and they made it dead easy.

The test suite ran smoothly other than tests for WebSockets which were broken due to some reason.
But I prefer to silence them, for now, to stay focused on what matters the most - getting rid of Travis.

The next hurdle was updating code coverage to coveralls.io. As before, I started from a web search -
"coveralls GitHub action". The first result in the web search was of a GitHub action for coveralls
residing in the [coverallsapp organization](https://github.com/coverallsapp/github-action).
Being an official action, I thought my journey ahead would be a cakewalk. To my disappointment, it
did not work as expected. My fallback was another web search "coveralls python github action".
This time I was greeted with an unofficial action that did not work. I remembered that
tests are run using the `coverage` package. I read through the documentation of the coverage module but
could not find anything there. Being frustrated I started doing random web searches and was greeted
with the python module of coveralls. And again, the developers made it dead easy for setting it up
on GitHub Actions. They had documented gotchas while using coveralls on GitHub Action. Huge respect
for developers of the coveralls python package.

The last step was to disable the `fail-fast` configuration of parallel builds. I deliberately left
it for the end because I knew it would be something well documented and as expected it was.

---------------------------------

TLDR; Read the documentation before jumping into the code.
