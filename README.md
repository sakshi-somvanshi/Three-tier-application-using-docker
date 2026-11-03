# Three-Tier Student Management Application

### Docker | Docker Compose | AWS EC2 | Nginx | Python Flask | PostgreSQL

## 1. Project Overview

The Three-Tier Student Management Application is a web-based application deployed on AWS EC2 using Docker Compose.

It follows a three-tier architecture:

- *Frontend:* HTML, CSS, JavaScript and Nginx
- *Backend:* Python Flask and Gunicorn
- *Database:* PostgreSQL 16

Users can add, view, update and delete student records through the web interface.

Nginx works as a reverse proxy and forwards API requests to the Flask backend. The backend communicates with PostgreSQL through a private Docker network.

## 2. Live Application

*Application URL:*  
http://43.205.125.88:3000

## 3. Architecture

text
                   USER / BROWSER
                         |
                         |
                    HTTP :3000
                         |
                         v
              FRONTEND - NGINX
              HTML | CSS | JavaScript
                         |
                         |
                   /api (Proxy)
                         |
                         v
              BACKEND - FLASK
               Python + Gunicorn
                    REST API
                         |
                         |
                    SQL :5432
                         |
                         v
                 POSTGRESQL 16
                   Database
                         |
                         v
                  DOCKER VOLUME
                  Persistent Data


       All containers communicate through:

          Docker Compose Network
                 mynetwork


## 4. Technologies Used

| Component | Technology |
|---|---|
| Cloud Platform | AWS EC2 |
| Operating System | Ubuntu |
| Containerization | Docker |
| Container Management | Docker Compose |
| Frontend | HTML, CSS, JavaScript |
| Web Server | Nginx |
| Backend | Python Flask |
| Application Server | Gunicorn |
| Database | PostgreSQL 16 |
| Version Control | Git and GitHub |

## 5. Project Features

- Three-tier application architecture
- Student management system
- Create student records
- View student records
- Update student records
- Delete student records
- REST API using Flask
- Nginx reverse proxy configuration
- Dockerized frontend, backend and database
- Docker Compose networking
- Persistent database storage using Docker volume
- Deployment on AWS EC2 Ubuntu

## 6. Project Architecture Explanation

### Frontend Layer

The frontend provides the user interface.

Technologies:
- HTML
- CSS
- JavaScript
- Nginx Alpine

Nginx serves the frontend files and forwards API requests to the backend.

### Backend Layer

The backend handles application logic and API requests.

Technologies:
- Python
- Flask
- Gunicorn

It processes student-related operations and communicates with the PostgreSQL database.

### Database Layer

PostgreSQL stores student information.

Technologies:
- PostgreSQL 16
- Docker Volume

The Docker volume helps preserve database data when containers are recreated.

## 7. Deployment on AWS EC2

### Step 1: Launch EC2 Instance

- Open AWS Management Console.
- Launch an Ubuntu EC2 instance.
- Create or select a key pair.
- Configure the Security Group.

### Step 2: Connect to EC2

Connect to the Ubuntu instance using SSH.

bash
ssh -i your-key.pem ubuntu@YOUR_EC2_PUBLIC_IP


### Step 3: Update Ubuntu

bash
sudo apt update
sudo apt upgrade -y


### Step 4: Install Docker

bash
sudo apt install docker.io docker-compose-v2 -y


Start Docker:

bash
sudo systemctl enable --now docker


Check versions:

bash
docker --version
docker compose version


### Step 5: Clone GitHub Repository

bash
git clone YOUR_GITHUB_REPOSITORY_URL


Go inside the project folder:

bash
cd YOUR_PROJECT_FOLDER


### Step 6: Configure Database Environment

Create the database environment file:

bash
nano database/.env


Add:

env
POSTGRES_DB=studentdb
POSTGRES_USER=admin
POSTGRES_PASSWORD=YOUR_STRONG_PASSWORD


### Step 7: Configure Backend Environment

Create the backend environment file:

bash
nano backend/.env


Add:

env
DB_HOST=postgres
DB_PORT=5432
DB_NAME=studentdb
DB_USERNAME=admin
DB_PASSWORD=YOUR_STRONG_PASSWORD
DB_SSLMODE=disable


Use the same database password in both environment files.

### Step 8: Configure Nginx Reverse Proxy

The frontend uses Nginx to forward API requests to the backend.

nginx
server {
    listen 80;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }

    location /api/ {
        proxy_pass http://backend:5000/;
    }
}


### Step 9: Build and Start Containers

Run from the project root directory:

bash
sudo docker compose up -d --build


### Step 10: Check Running Containers

bash
sudo docker compose ps


### Step 11: Test API

Check backend:

bash
curl http://localhost:5000/health


Check student records:

bash
curl http://localhost:3000/api/students


### Step 12: Access Application

Open the application in your browser:

text
http://YOUR_EC2_PUBLIC_IP:3000


## 8. Docker Commands

Check running containers:

bash
sudo docker compose ps


View all container logs:

bash
sudo docker compose logs -f


View backend logs:

bash
sudo docker compose logs backend


View frontend logs:

bash
sudo docker compose logs frontend


Restart containers:

bash
sudo docker compose restart


Stop containers:

bash
sudo docker compose down


Rebuild application:

bash
sudo docker compose up -d --build


*Note:* Avoid using docker compose down -v unless you intentionally want to delete the database volume and its stored data.

## 9. API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | /api/students | Get all students |
| POST | /api/students | Add a student |
| GET | /api/students/{id} | Get student by ID |
| PATCH | /api/students/{id} | Update student |
| DELETE | /api/students/{id} | Delete student |

## 10. AWS Security Group

| Port | Service | Access |
|---|---|---|
| 22 | SSH | My IP |
| 3000 | Frontend | Public access |
| 5000 | Backend | Internal Docker network |
| 5432 | PostgreSQL | Internal Docker network |

*Security Note:* Backend port 5000 and PostgreSQL port 5432 should not be publicly exposed.

## 11. Important Learnings

Through this project, I gained practical experience in:

- Deploying applications on AWS EC2.
- Creating Docker images and containers.
- Managing multiple services using Docker Compose.
- Configuring Nginx as a reverse proxy.
- Connecting Flask applications with PostgreSQL.
- Configuring Docker networks and volumes.
- Troubleshooting container and application issues.
- Deploying a three-tier application on AWS.

## 12. Future Improvements

- Add HTTPS using SSL/TLS.
- Implement user authentication.
- Add monitoring and logging.
- Configure automated deployment.
- Improve application security.

## 13. Author

*Sakshi Somvanshi*

Electronics and Telecommunication Engineering Graduate

GitHub:  
https://github.com/sakshi-somvanshi

---

*Project:* Three-Tier Student Management Application  
*Platform:* AWS EC2  
*Containerization:* Docker Compose