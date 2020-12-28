---
title: 'Hacking Django: Follow Up'
published: true
---

In the previous attempt to add a custom landing page for a logged-in user in
Django admin, I ended up writing hacky code. I asked on the Django Developers
mailing list whether it will be fruitful to add a dedicated setting in Django
to allow that.

A fellow Django contributor answered my query that it is already possible to do
that by overriding the `login` view.

```python
def login(self, *args, **kwargs):
        response = super().login(*args, **kwargs)
        if isinstance(response, HttpResponseRedirect):
            response = HttpResponseRedirect("/custom-page/")
        return response
```

The above code looks way better than my implementation. But I don’t know
whether this is what I want.
