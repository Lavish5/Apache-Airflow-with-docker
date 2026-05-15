# Apache Airflow With Docker

This project sets up a local Apache Airflow environment using Docker Compose. It runs Airflow with a PostgreSQL metadata database, making it easy to practice DAG development, scheduling, and workflow orchestration without installing Airflow directly on your machine.

## Tech Stack

- Apache Airflow
- Docker
- Docker Compose
- PostgreSQL
- LocalExecutor

## Project Structure

```bash
Apache-Airflow-with-docker/
|-- docker-compose.yml
|-- dags/
`-- README.md
```

> The `dags/` folder is mounted into the Airflow containers at `/opt/airflow/dags`. Add your DAG Python files there.

## Prerequisites

Make sure you have these installed:

- Docker Desktop
- Docker Compose

Check your installation:

```bash
docker --version
docker compose version
```

## Getting Started

Clone the repository and move into the project folder:

```bash
git clone <your-repository-url>
cd Apache-Airflow-with-docker
```

Create the DAGs folder if it does not already exist:

```bash
mkdir dags
```

Start the containers:

```bash
docker compose up -d
```

Initialize the Airflow metadata database:

```bash
docker compose run --rm webserver airflow db migrate
```

Create an Airflow admin user:

```bash
docker compose run --rm webserver airflow users create --username admin --firstname Lavish --lastname Jain --role Admin --email admin@example.com --password admin
```

Restart the services:

```bash
docker compose restart
```

## Access Airflow

Open Airflow in your browser:

```bash
http://localhost:8080
```

Default login:

- Username: `admin`
- Password: `admin`

## Services

| Service | Description | Port |
| --- | --- | --- |
| `postgres` | Airflow metadata database | `5432` |
| `webserver` | Airflow web UI | `8080` |
| `scheduler` | Runs and schedules DAG tasks | N/A |

## Useful Commands

Start all services:

```bash
docker compose up -d
```

Stop all services:

```bash
docker compose down
```

View logs:

```bash
docker compose logs -f
```

View Airflow webserver logs:

```bash
docker compose logs -f webserver
```

View scheduler logs:

```bash
docker compose logs -f scheduler
```

List running containers:

```bash
docker compose ps
```

## Adding a DAG

Create a Python file inside the `dags/` folder:

```bash
dags/example_dag.py
```

Airflow will automatically scan the folder and show valid DAGs in the UI.

## Reset Environment

To stop the containers and remove the PostgreSQL volume:

```bash
docker compose down -v
```

Use this when you want a fresh Airflow metadata database.

## Notes

- This setup is for local learning and development.
- The Docker Compose file uses `apache/airflow:latest`; for production-like projects, pin a specific Airflow version.
- PostgreSQL data is stored in the `postgres_data` Docker volume.
