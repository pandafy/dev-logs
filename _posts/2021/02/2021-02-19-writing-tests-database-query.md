---
title: Writing tests for Database Queries
---

While working on a [pull request](https://github.com/kiwitcms/Kiwi/pull/2255)
to add automated tests for a Django admin class for Kiwi TCMS, I had to write
automated tests to check whether `select_related` queries were being executed
properly.

From my experience of writing tests for OpenWISP, I used `assertNumQueries` of
Django’s `TransactionTestCase` class which records the number of database
queries made under its context.

From my manual testing, I verified that more queries were being executed when
`select_related` is not used. I based the tests on my findings. But the
maintainer did not like this approach. He raised a concern that
`assertNumQueries` acts as a black box and this test will fail if any changes
are made to Django’s internals.

The maintainer suggested to make tests more robust such that it will check
whether the exact database query is being executed or not. After basing my
work on an example he shared, I wrote up the following code:

```python
with CaptureQueriesContext(connection) as context:
    self.client.get(reverse("admin:management_component_changelist"))
    for query in context.captured_queries:
        if expected_query == query["sql"]:
            break
    else:
        self.fail("Component select related query not found.")
```
