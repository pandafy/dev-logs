---
title: Deferred Fields in Django
---

Django's ORM provides a way to load only specific fields from the database using
`only` and `defer` methods. The deferred fields are represented with
the `django.db.models.base.DEFERRED` object.

`refresh_from_db` model loads the deferred fields from the database, but
it is possible to make it load only specific fields.

While working on the openwisp-controller, I learn the shenanigans of deferred
fields. openwisp-controller needs to emit signals when some specific fields
are implemented. Some of these fields are sometimes deferred, hence I had to
write special code to fetch these fields from the database if they are no
longer deferred. What does that mean? Let me explain it through an example.

Consider a Django model `Person` containing two fields, name and age.
Now, you queried this model loading only the `name` field

```
first_person = Person.objects.only('name').first()
```

This makes the `age` field deferred. How can you check this? Well, if you
access the `age` field as `first_person.age`, Django will fetch the value
from the database for you. Therefore, a special method `get_deferred_fields()`
is provided which returns a set of deferred fields for the instance of the
model.

Executing `first_person.get_deferred_fields()` should return `{'age'}`. But
if you assign a value to the age attribute like `first_person.age = 99`, you
will get an empty set from `first_person.get_deferred_fields()`
signalling that there are no deferred fields  of `first_person` instance.

Following pages Django's documentation describe deferred fields well:
- https://docs.djangoproject.com/en/3.2/ref/models/querysets/
- https://docs.djangoproject.com/en/3.2/ref/models/instances/
