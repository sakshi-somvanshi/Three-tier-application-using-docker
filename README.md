# Three-Tier Student Management Application (Docker + AWS EC2)

A containerized three-tier web application for managing student records. The frontend, backend API and PostgreSQL database run in separate Docker containers, orchestrated with Docker Compose and deployed on an AWS EC2 instance.

*Live demo (while EC2 is running):* http://43.205.125.88:3000

## Architecture

mermaid
flowchart LR
    U[Browser] -->|HTTP :3000| FE[Frontend<br/>Nginx Alpine]
    U -->|REST API :5000| BE[Backend<br/>Python + Flask + Gunicorn]
    BE -->|SQL :5432| DB[(PostgreSQL 16)]
    DB --- V[(Volume: pgdata)]


| Tier | Technology | Container | Host Port |
|------|-----------|-----------|-----------|
| Presentation | HTML, CSS, JavaScript, Nginx | my-frontend-container | 3000 |
| Application | Python, Flask, Gunicorn | my-python-container | 5000 |
| Data | PostgreSQL 16 | my_postgres | internal only |

All services share a user-defined bridge network (mynetwork) and talk to each other using container names. Database data is persisted in the named volume pgdata.

## Features

- Add, view, update and delete student records (CRUD)
- REST API built with Flask
- Database tables created automatically on first start (create_table.sql)
- PostgreSQL health check; backend starts only after the database is healthy
- GitHub Actions workflows that build and push images to Docker Hub

## Tech Stack

| Area | Tools |
|------|-------|
| Frontend | HTML, CSS, JavaScript, Nginx |
| Backend | Python, Flask, Flask-CORS, psycopg2, Gunicorn |
| Database | PostgreSQL 16 |
| DevOps | Docker, Docker Compose, GitHub Actions |
| Cloud | AWS EC2 (Ubuntu) |

## Project Structure

text
Three-Tier-Application/
├── .github/workflows/
│   ├── backend-workflow.yml
│   └── frontend-workflow.yml
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── database/
│   ├── create_table.sql
│   └── Dockerfile
├── frontend/
│   ├── index.html
│   ├── app.js
│   ├── style.css
│   └── Dockerfile
├── screenshots/
├── docker-compose.yaml
├── cmd.md
├── compose-cmd.md
└── README.md


## Environment Variables

.env files are *not committed* to Git (see .gitignore). Create them manually on every machine.

*database/.env*
env
POSTGRES_USER=<db-user>
POSTGRES_PASSWORD=<strong-password>
POSTGRES_DB=<db-name>


*backend/.env*
env
DB_HOST=my_postgres
DB_PORT=5432
DB_NAME=<db-name>
DB_USERNAME=<db-user>
DB_PASSWORD=<strong-password>
DB_SSLMODE=prefer
CORS_ORIGINS=http://43.205.125.88:3000


> Database name, user and password must be identical in both files.

In frontend/app.js, set the backend URL:
javascript
const API_URL = "http://43.205.125.88:5000"


## Run Locally

Prerequisite: Docker Desktop.

bash
git clone https://github.com/sakshi-somvanshi/Three-Tier-Application.git
cd Three-Tier-Application


1. Create database/.env and backend/.env
2. Set API_URL to http://localhost:5000 in frontend/app.js
3. Set CORS_ORIGINS=http://localhost:3000 in backend/.env

bash
docker compose up -d --build
docker compose ps


Open http://localhost:3000

## Deploy on AWS EC2

1. *Launch an EC2 instance* (Ubuntu, t2/t3.micro) with inbound rules:
   - 22 (SSH, your IP only)
   - 3000 (frontend)
   - 5000 (backend API)

2. *Connect via SSH*
   bash
   ssh -i <key>.pem ubuntu@43.205.125.88
   

3. *Install Docker and Git*
   bash
   sudo apt update
   sudo apt install docker.io docker-compose-v2 git -y
   sudo systemctl enable --now docker
   sudo usermod -aG docker ubuntu
   
   Log out and log in again.

4. *Clone and configure*
   bash
   git clone https://github.com/sakshi-somvanshi/Three-Tier-Application.git
   cd Three-Tier-Application
   nano database/.env
   nano backend/.env
   nano frontend/app.js
   

5. *Start the application*
   bash
   docker compose up -d --build
   docker compose ps
   

6. *Open in browser:* http://43.205.125.88:3000

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /students | List all students |
| POST | /students | Add a student |
| PATCH | /students/<id> | Update a student |
| DELETE | /students/<id> | Delete a student |

## CI/CD with GitHub Actions

Two workflows build the backend and frontend images and push them to Docker Hub when code changes on main.

Required repository secrets (Settings → Secrets and variables → Actions):

| Secret | Value |
|--------|-------|
| DOCKER_USERNAME | Docker Hub username |
| DOCKER_ACCESS_TOKEN | Docker Hub access token |

## Useful Commands

bash
docker compose ps                  # container status
docker compose logs backend        # backend logs
docker compose restart backend     # restart a service
docker compose down                # stop and remove containers
docker compose down -v             # also remove the database volume
docker exec -it my_postgres psql -U <db-user> -d <db-name>


More commands: [cmd.md](cmd.md) and [compose-cmd.md](compose-cmd.md).

## Screenshots

| Step | Screenshot |
|------|-----------|
| Application dashboard | 

![App](screenshots/app.png)

 |
| Running containers | 

![Containers](screenshots/docker-ps.png)

 |
| GitHub Actions success | 

![CI](screenshots/actions.png)

 |

## Security Notes

- Never commit .env files or real passwords (excluded via .gitignore).
- Use strong database passwords in production.
- Restrict SSH (port 22) to your own IP in the Security Group.
- The EC2 public IP changes after a stop/start. Update API_URL and CORS_ORIGINS, or attach an Elastic IP.

## Key Learnings

- Splitting an application into frontend, backend and database tiers
- Writing Dockerfiles and building images
- Docker networking with a custom bridge network
- Persisting data with Docker volumes
- Orchestrating services with Docker Compose, health checks and depends_on
- Managing configuration with environment files
- Automating image builds with GitHub Actions
- Deploying and troubleshooting a containerized app on AWS EC2

## Future Improvements

- Add an Nginx reverse proxy so the browser only talks to one port
- Add HTTPS with a domain and TLS certificate
- Attach an Elastic IP and automate deployment from CI
- Add input validation and unit tests for the API

## Author

*Sakshi Somvanshi*
GitHub: [@sakshi-somvanshi](https://github.com/sakshi-somvanshi)