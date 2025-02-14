# ELT Pipeline with dbt and Airflow

## Overview
This project implements an **ELT (Extract, Load, Transform) pipeline** using **dbt** and **Airflow**. The pipeline extracts data from a source PostgreSQL database, loads it into a destination PostgreSQL database, and transforms it using dbt models. Airflow orchestrates the workflow to ensure smooth execution and scheduling.

## Architecture
The pipeline consists of the following components:
- **PostgreSQL (Source & Destination)**: Stores raw and transformed data.
- **Airflow**: Manages workflow orchestration and scheduling.
- **dbt**: Handles transformations within the destination database.
- **Docker & Docker Compose**: Provides containerized environments.

## Setup Instructions

### Prerequisites
Ensure you have the following installed:
- Docker & Docker Compose
- Git
- Python (if running locally)

### Installation
1. **Clone the Repository:**
   ```bash
   git clone <repository-url>
   cd elt_basics
   ```

2. **Start the Services:**
   ```bash
   docker-compose up -d
   ```
   This will start PostgreSQL, Airflow, and other necessary services.

3. **Initialize Airflow:**
   ```bash
   docker exec -it airflow-webserver airflow db init
   docker exec -it airflow-webserver airflow users create \
     --username admin --password admin \
     --firstname Air --lastname Flow --role Admin --email admin@example.com
   ```

4. **Run dbt Transformations:**
   ```bash
   docker exec -it dbt-container dbt run
   ```

5. **Trigger Airflow DAGs:**
   - Open Airflow UI: `http://localhost:8080`
   - Enable & Trigger DAG: `elt_dag`

## Project Structure

## Airflow DAG Overview
The **elt_dag** workflow follows these steps:
1. **Extract**: Dump data from the source PostgreSQL database.
2. **Load**: Load raw data into the destination database.
3. **Transform**: Run dbt models to clean and transform data.
4. **Validation**: Ensure transformations meet business logic.

## Troubleshooting
- If Airflow containers fail, restart them:
  ```bash
  docker-compose restart airflow-webserver airflow-scheduler
  ```
- If dbt fails due to connection issues, verify the database connection settings in `profiles.yml`.

## Contributing
Feel free to submit issues or pull requests if you’d like to contribute!



