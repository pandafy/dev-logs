---
title: Developing Configurable Component in Django
published: true
---

I like writing reusable code. What I like more is writing code for configurable
components. For this project, I wanted to develop a component that fetches data
from the database and create graphs and charts. It sounds easy, right? Well, it
was. But, it felt a bit challenging to me at first.

I was okay with configurable queries, it was very straightforward to implement
it. But, making those queries on configurable models was troubling me. I kind
of got stuck on this. And then, swappable models occurred to me. In OpenWISP,
we have used the `swapper` module to load models. The
[swapper module](https://github.com/wq/django-swappable-models) allows users to
replace the existing models with custom ones without any hassle. It took me a
while to wrap my head around swappable models.

The major hurdle was down and I had to just provide other properties for
querying the database. I provided the configuration of the query parameters as
below:

```python
CONFIG = [
    {
        'app_label': 'home',
        'model': 'orders',
        'aggregate_by': 'zone'
    }
]
```

The above configuration was processed by the following code to fetch data from
the database.

```python
data = {}
for entry in CONFIG:
    model = load_model(entry['app_label'],entry['model'])
    qs = model.objects.all().values(entry['aggregate_by']).annotate(
            count=Count(entry['aggregate_by'] )
        )
    data[entry[model_name]] = qs
```

The feature I was working on was concerned about the aggregated data,
hence the above code query accounts only for that. But, the query can be
enhanced by using a sub dictionary in the configuration and passing it along
in code as follows

```python
CONFIG = [
    {
        'app_label': 'home',
        'model': 'orders',
        'aggregate_by': 'zone'
        'query_params': {
            'order_date__lte': '2020-12-30'
        }
    }
]
```

The code for querying will be modified as below:

```python
    qs = model.objects.filter(**entry['query_params']).values(entry['aggregate_by']).annotate(
            count=Count(entry['aggregate_by'] )
        )
```

I will keep looking for ways to make the database query more configurable.

----------------

### In other news

Another round of triaging and reviews of PR in OpenWISP. But, today’s reviews
were not as comprehensive as I like. I don’t want to step on someone else’s
review cycle.
