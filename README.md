# Data Engineering Docker Workshop

This repository contains exercises for running a data engineering pipeline and
its supporting services with Docker.

## PostgreSQL and pgcli

The project uses a PostgreSQL 18 container as the database and `pgcli` as the
command-line client.

### Prerequisites

- Docker is installed and running.
- [`uv`](https://docs.astral.sh/uv/) is installed.
- The Python dependencies in `pipeline/pyproject.toml` are installed. From the
  repository root, run:

  ```bash
  cd pipeline
  uv sync --dev
  ```

### Start PostgreSQL

Run the following command in one terminal:

```bash
docker run -it --rm \
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v ny_taxi_postgres_data:/var/lib/postgresql \
  -p 5432:5432 \
  postgres:18
```

This command:

- creates a PostgreSQL user named `root` with password `root`;
- creates the `ny_taxi` database;
- exposes PostgreSQL on `localhost:5432`;
- stores the database files in the `ny_taxi_postgres_data` Docker volume, so
  the data remains available after the container is removed; and
- automatically removes the stopped container because of `--rm`.

Leave this terminal running while using the database. Press `Ctrl+C` to stop
PostgreSQL.

### Connect with pgcli

In another terminal, run the following from the `pipeline` directory:

```bash
uv run pgcli -h localhost -p 5432 -u root -d ny_taxi
```

When prompted, enter `root` as the password. You can verify the connection by
running:

```sql
SELECT version();
```

Enter `\q` to exit `pgcli`.
