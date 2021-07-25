---
title: "Django Query Expressions: F()"
---

The `F()` Django query expression allows performing a database operation on a
field without loading its value in memory. Using it, we can update values
for not only a particular object but also for an entire queryset.
To do that, we need to use `F()` in conjunction with the
`update()` method.

Following is an example from the Django documentation:

```python
Reporter.objects.all().update(stories_filed=F('stories_filed') + 1)
```

The `F()` expressions helps improving performance by reducing the number of
database queries generated as well as by offloading the processing chore to the database.

I got to learn about `F()` expressions when I needed to provide an alias to a
database field in
[openwisp-controller](https://github.com/openwisp/openwisp-controller/blob/32ccea8aef9c25492b5060e1a1fd9607a9cead58/openwisp_controller/config/api/views.py#L194-L208).
Not only this, `F()` expressions can also be used to create dynamic fields
containing values from combining existing fields.

As with every other aspect of Django, usage of `F()` expressions has been clearly
documented in [Django's documentation for "Query
Expressions"](https://docs.djangoproject.com/en/3.2/ref/models/expressions/#f-expressions).

