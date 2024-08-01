Run locally with metadata:

```datasette psephology.db --metadata metadata.json```

Publishing to Heroku:

```datasette publish heroku psephology.db --metadata metadata.json --name psephology-datasette```

Convert postgresql to sqlite: https://datasette.io/tools/db-to-sqlite

```db-to-sqlite "postgresql://localhost/psephology" psephology.db --all```

Dropping a db in Postgres and then importing a dump:

```dropdb psephology```

... in psql:

```\i dump_name.sql```
