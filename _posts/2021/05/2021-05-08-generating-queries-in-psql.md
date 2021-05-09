---
title: Generating queries in PSQL
---

I was interacting today with a Postgres server where I needed to change the
owner of all of the tables of a database. An answer on StackOverflow suggested
the following code which transfers ownership of call of the public tables.

```
SELECT 'ALTER TABLE '|| schemaname || '."' || tablename ||'" OWNER TO new_owner;'
FROM pg_tables WHERE NOT schemaname IN ('pg_catalog', 'information_schema')
ORDER BY schemaname, tablename;
```

The above code does not transfer the ownership, but generates queries that
can be executed to transfer ownership. It might be possible that I didn’t read
the whole answer and copied only this part. But it is so much better to verify
the queries before executing them.

I was unaware that it is possible to generate queries in PSQL. This made me want to dust off my DBMS skills and read Database System Concepts by Henry F. Korth et al again.
