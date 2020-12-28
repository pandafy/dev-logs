---
title: Hacking Django
published: true
---

The one thing I like most about the Django framework is that it is notoriously
easy to hack.

I was looking for a way to add a custom landing page for Django Admin. As
usual, I started with the documentation. Django provides a way to add a custom
index page for the admin site. But using that setting will destroy the default
index page of Django admin.

The next step was to look into the code. I was looking for a configurable
setting through which I could redirect the user to my custom landing page
instead of the Django admin’s index page.

Failing to find a neat way to patch the code, I fallback to the basic OOPs
concept. I was going to override the default index view of Django’s `AdminSite`
class.

This is the code that I end up writing:

```python
def django_index(self, request, extra_context=None):
        return super().index(request, extra_context)

    def index(self, request, extra_context=None):
        return render(request, 'landing_page.html')
```

The above code does not do anything interesting, but I am sure that other
developers will find it stupid. It calls the `index` method of the base class
from another method and overrides the `index` method in the derived `AdminSite`
class.
