Run locally with metadata:

```datasette psephology.db --metadata metadata.json```

Publishing to Heroku:

```datasette publish heroku psephology.db --metadata metadata.json -n psephology-datasette --setting sql_time_limit_ms 3500 --setting max_returned_rows 5000```

Convert postgresql to sqlite: https://datasette.io/tools/db-to-sqlite

```db-to-sqlite "postgresql://localhost/psephology" psephology.db --all```