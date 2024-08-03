Run locally with metadata:

```datasette psephology.db --metadata metadata.json```

Publishing to Heroku:

```datasette publish heroku psephology.db --metadata metadata.json --name psephology-datasette```

Convert postgresql to sqlite: https://datasette.io/tools/db-to-sqlite

psql: drop database psephology;
psql: create database psephology;
psql psephology < db/dumps/2024-08-01.sql

```db-to-sqlite "postgresql://localhost/psephology" psephology.db --all```
