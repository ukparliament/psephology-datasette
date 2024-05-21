Publishing to Heroku:

datasette publish heroku psephology.db --metadata metadata.json -n psephology-datasette

Convert postgresql to sqlite: https://datasette.io/tools/db-to-sqlite

db-to-sqlite "postgresql://localhost/psephology" psephology.db --all