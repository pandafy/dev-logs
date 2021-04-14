---
title: Testing delete endpoint of Django Admin
---

I had to write a test today that involved testing the `delete` endpoint of
Django admin. But just after writing the first few lines of the test, I
realized that Django displays a confirmation page before actually deleting the
object. And since the test suite of Django does not offer a JavaScript runtime,
I wondered how I could follow the delete confirmation.

I looked for references inside OpenWISP’s codebase but couldn’t find anything.
Then I resort to diving into Django’s code and voila, I got my answer.

Instead of a `GET` request, I just needed to send a `POST` request with
`{'post': 'yes'}` payload to the delete endpoint of the object.

Django’s codebase is a treasure.


