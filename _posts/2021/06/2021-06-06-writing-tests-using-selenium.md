---
title: Writing tests using Selenium
---

I have been working on relevant templates features of openwisp-controller
on-and-off for the last couple of months. The goal is to only show templates
that can be applied to the device. Every time I made an improvement, something
broke. Being implemented in JavaScript, it didn’t have any automated tests and
my manual testing, let’s say, was not holistic. But it was time to change this.

This was my first time writing testing for UI using selenium. Luckily,
`dockerize-openwisp` already has some tests for UI so I took them as reference.

I learn something new about Django almost every day while working on OpenWISP
and this week was no different. Django provides a
[`LiveServerTestCase`](https://docs.djangoproject.com/en/3.2/topics/testing/tools/#django.test.LiveServerTestCase)
class. It behaves just like `TransactionTestCase` but also launches a live
Django server in the background. Due to this live server, it is possible to make
UI testing a part of the existing test suite.

But there was a catch. `LiverServerTestCase` uses two different threads, one for
the live server and another for running the test case. This multi-threaded
nature does not play well with the in-memory SQLite database used for running
tests in openwisp-controller. The two threads share the same connection to the
database, hence errors like “database locked” popped up when both threads tried
to access the database at the same time. This was happening frequently at
`tearDown` of a test when the database is rolled back to a clean state. With a
little bit of tinkering, I ensured that the live server was not executing any
query on the database by adding a delay after selenium is done testing actions.
This was a suggestion given in Django's documentation and it worked.
