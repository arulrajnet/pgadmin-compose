# pgAdmin Docker Compose Setup

This project provides a Docker Compose configuration to deploy **pgAdmin 4** alongside a **PostgreSQL** database. It includes an initialization container to securely handle password files.

## Features

- **Automated Password File Creation**: An `init-pgpass` container creates the `pgpass` file with correct permissions (0600) and ownership.
- **Shared Volume**: The `pgpass` file is shared securely between the init container and pgAdmin.
- **Service Dependency**: pgAdmin waits for the init container to complete successfully before starting.
- **Configuration**:
    - Pre-configured server list via `servers.json`.
    - `PGADMIN_CONFIG_MASTER_PASSWORD_REQUIRED` set to `False` (no login required).

## Prerequisites

- Docker
- Docker Compose

## Configuration

The setup is controlled via the `.env` file. Modify the following variables as needed:

```env
# Postgres Connection Details
POSTGRES_HOST=pgsql          # Hostname of the Postgres service (default: pgsql)
POSTGRES_PORT=5432           # Port (default: 5432)
POSTGRES_USER=postgres       # Username
POSTGRES_PASSWORD=postgres   # Password
POSTGRES_DB=postgres         # Database name
```

## Usage

1.  **Clone the repository** (if applicable) or navigate to the directory.

2.  **Start the services**:
    ```bash
    docker-compose up -d
    ```

3.  **Access pgAdmin**:
    Open your browser and navigate to [http://localhost:38001](http://localhost:38001).

    *Note: Since master password is disabled, you should be logged in automatically or prompt for no credentials.*

## Architecture

- **pgsql**: The PostgreSQL database service.
- **init-pgpass**: A transient Alpine container that generates `/pgpass-writable/pgpass` from environment variables.
- **pgadmin**: The main pgAdmin 4 service. It mounts the `pgpass` file and the `servers.json` config.

## Author

<p align="center">
  <a href="https://x.com/arulrajnet">
    <img src="https://github.com/arulrajnet.png?size=100" alt="Arulraj V" width="100" height="100" style="border-radius: 50%;" class="avatar-user">
  </a>
  <br>
  <strong>Arul</strong>
  <br>
  <a href="https://x.com/arulrajnet">
    <img src="https://img.shields.io/badge/Follow-%40arulrajnet-1DA1F2?style=for-the-badge&logo=x&logoColor=white" alt="Follow @arulrajnet on X">
  </a>
  <a href="https://github.com/arulrajnet">
    <img src="https://img.shields.io/badge/GitHub-arulrajnet-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub @arulrajnet">
  </a>
  <a href="https://linkedin.com/in/arulrajnet">
    <img src="https://custom-icon-badges.demolab.com/badge/LinkedIn-arulrajnet-0A66C2?style=for-the-badge&logo=linkedin-white&logoColor=white" alt="LinkedIn @arulrajnet">
  </a>
</p>
