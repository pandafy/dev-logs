---
title: Executing Raw SQL in Django
---

Django provides a way to directly execute SQL queries which is neatly described
in [Django
documentation](https://docs.djangoproject.com/en/3.2/topics/db/sql/#django.db.models.Manager.raw).
This devlog summarizes my key takeaways while working with it.

The `Manager.raw` method supports deferring unrequired fields. But it is to
be noted that the primary key can't be deferred since it is used by Django
to identity model instances. Interestingly, a `FieldDoesNotExist` exception is
raised if you try to skip the primary key field.

`Manager.raw` also allows using placeholders like `%s` to allow dynamic SQL
queries. It has been recommended to use the `params` argument of `Manager.raw`
to supply values for these placeholders instead of using string formatting
provided by Python. Doing so can make the application prone to SQL
injection attacks.

There is a caveat while working with placeholders in raw SQL queries. For
SQLite the placeholder key is `%%s` while for PostgreSQL it is `%s`. Django
does not automatically handle the two cases and it is up to the developer to take
care of it.
