---
layout: post
title: "Migrating Grafana SQLite Database to PostgreSQL"
---

To migrate your SQLite database to PostgreSQL, you can use `pgloader`. Follow these steps to complete the migration:

- First, acquire the Grafana PostgreSQL schema from a test environment. The schema for Grafana version 12.0.1 is available at the following link: [Grafana PostgreSQL Schema](https://gist.github.com/dedunumax/fe3cd4affb7f44ba097d605d693bd633).
- Save the schema as `grafana.sql`.

- Use the `psql` command to restore the schema into your PostgreSQL database:

```bash
psql -h localhost -p 5432 -U postgres -d grafana -f grafana.sql
```

- Install `pgloader` using Homebrew:

```bash
brew install pgloader
```

- Create a file named `grafana.load` with the following content to define the migration process:

```sql
load database
from '/Users/john/path/to/grafana-sqlite.db'
into postgresql:///grafana:password@localhost:5432/grafana

with data only, reset sequences
set work_mem to '16MB', maintenance_work_mem to '512 MB';
```

- Execute the migration using `pgloader`:

```bash
pgloader grafana.load
```

- Update your Grafana configuration to point to the new PostgreSQL database:

```bash
GRAFANA_DATABASE_HOST=localhost
GRAFANA_DATABASE_PORT=5432
GRAFANA_DATABASE_USER=grafana
GRAFANA_DATABASE_PASSWORD=password
GRAFANA_DATABASE_NAME=grafana
```

- Finally, restart the Grafana server to apply the changes:

```bash
sudo systemctl restart grafana-server
```

By following these steps, you will successfully migrate your Grafana SQLite database to PostgreSQL.

Note: LLMs were harmed in the making of this document.

### Tags

- postgresql
- sqlite
- grafana
- migration