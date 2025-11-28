# Psephology Datasette

This repo looks after the set up and hosting of a [Datasette](https://datasette.io/) instance for the Psephology database. Datasette is a nice front end for browsing data sets.

## Run locally with metadata:

### Set up venv

 * `pip install virtualenv`
 * `python3 -m venv ./venv`
 * `source venv/bin/activate`

### Then

 * install python
 * activate `venv` by doing `source venv/bin/activate`
 * install dependencies by doing `pip install -r requirements.txt`
 * Run datasette - ```datasette psephology.db --metadata metadata.json```

## GitHub action

A [github action](.github/workflows/datasette-build-and-deploy.yml) runs on a schedule, publishing the datasette with the latest copy of the database. This also runs on a push or a branch push.

### What the action does

 * Set up Python
 * Install dependencies
 * Remove old database file - if you don't do this, the `db-to-sqlite` seems to append to the existing database.
 * Run `db-to-sqlite` against the Heroku Psephology Postgres database - credentials are stored as an action secret - settable by repo admins
 * Add a deploy timestamp file - useful for debugging and forcing a push
 * Commit updated database to the repository
 * Authenticate with Heroku using a Heroku api key - stored as an action secret
 * Publish using `datasette publish` to Heroku

 ### notes on the GH action

 * `datasette publish` is hardcoded to deploy using Python 3.11 rather than whatever is set in the repo. This confuses matters!
 * The action checks out the `main` branch, not a different one if you are working on a different one. Bear this in mind if doing PRs! If you don't specify a branch to check out, you ended up with a detached head state, no fun for anyone.

## Local publishing to Heroku:

```datasette publish heroku psephology.db --metadata metadata.json --name psephology-datasette```

## Local convert postgresql to sqlite: https://datasette.io/tools/db-to-sqlite

```
psql: drop database psephology;
psql: create database psephology;
psql psephology < db/dumps/2024-08-01.sql
```

```db-to-sqlite "postgresql://localhost/psephology" psephology.db --all```

## Local dropping a db in Postgres and then importing a dump:

```dropdb psephology```

... in psql:

```\i dump_name.sql```
