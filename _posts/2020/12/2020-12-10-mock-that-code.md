---
title: Mock that code
published: true
---

I woke up early to work on a  Kiwi TCMS issue.
The [issue was to write tests for the `SafeJSONRPCHandler`]()
that escapes the HTML to prevent XSS attacks. The test suite of Kiwi TCMS has
an XML-RPC client only. While starting with the issue, I was trying to mimic
tests written with an XML-RPC client.

I did my fair amount of research for adding a JSON-RPC client, but it required
a new module to be added to the dependency. I asked the maintainer for the
best course of action to write tests.

The maintainer suggested mocking the part of the code which was being
inherited from the `django-modern-rpc` module’s `JSONRPCHandler` class.
I had thought about it before but didn’t proceed because I was afraid that the
maintainer would complain that such tests just increase coverage.

With a green signal from the maintainer, I mocked methods of the parent class,
wrote the tests, and opened a PR in less than an hour. Except for the time
when I was calling the method of the base class instead of
`SafeJSONRPCHandler`.

As a surprise, my PR got merged without any requested changes. Swish! This was
the first time my PR to Kiwi TCMS got merged without any requested changes.

-----------------

### In other news

I had a couple of meetings today, so most of my day was spent in them. I also
added a favicon to [my devlogs website](https://pandafy.me) today.
It took me more time than expected to add them.
