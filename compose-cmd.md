# Docker Compose Commands

## 1. Check Docker Compose Version

bash
docker compose version


## 2. Start All Services

bash
sudo docker compose up -d


## 3. Build and Start All Services

bash
sudo docker compose up -d --build


## 4. Check Running Services

bash
sudo docker compose ps


## 5. Check All Services

bash
sudo docker compose ps -a


## 6. View All Container Logs

bash
sudo docker compose logs


## 7. Follow Live Logs

bash
sudo docker compose logs -f


## 8. View Frontend Logs

bash
sudo docker compose logs frontend


## 9. View Backend Logs

bash
sudo docker compose logs backend


## 10. View Database Logs

bash
sudo docker compose logs postgres


## 11. Restart All Services

bash
sudo docker compose restart


## 12. Restart Frontend

bash
sudo docker compose restart frontend


## 13. Restart Backend

bash
sudo docker compose restart backend


## 14. Restart Database

bash
sudo docker compose restart postgres


## 15. Stop All Services

bash
sudo docker compose stop


## 16. Start Stopped Services

bash
sudo docker compose start


## 17. Stop and Remove Containers

bash
sudo docker compose down


## 18. Rebuild Frontend

bash
sudo docker compose build frontend


## 19. Rebuild Backend

bash
sudo docker compose build backend


## 20. Rebuild and Restart Frontend

bash
sudo docker compose up -d --build frontend


## 21. Rebuild and Restart Backend

bash
sudo docker compose up -d --build backend


## 22. Execute Command Inside Backend

bash
sudo docker compose exec backend sh


## 23. Execute Command Inside Database

bash
sudo docker compose exec postgres psql -U admin -d studentdb


## 24. Check Backend Health

bash
curl http://localhost:5000/health


## 25. Check Application Through Nginx

bash
curl http://localhost:3000/api/students


## 26. Check Student Records

bash
curl http://localhost:3000/api/students


## 27. Check Docker Compose Configuration

bash
sudo docker compose config


## 28. Check Docker Compose Services

bash
sudo docker compose config --services


---

# Project Services

| Service | Technology | Container |
|---|---|---|
| Frontend | HTML, CSS, JavaScript, Nginx | my-frontend-container |
| Backend | Python, Flask, Gunicorn | my-python-container |
| Database | PostgreSQL 16 | my_postgres |

# Project Details

*Project:* Three-Tier Student Management Application

*Author:* Sakshi Somvanshi

*Cloud Platform:* AWS EC2

*Containerization:* Docker

*Orchestration:* Docker Compose

*Network:* mynetwork

*Volume:* pgdata

*Application URL:* http://43.205.125.88:3000

---

## Important Notes

- Run Docker Compose commands from the project directory containing compose.yaml or docker-compose.yml.
- docker compose down removes containers and networks but keeps named volumes.
- docker compose down -v also deletes volumes and can permanently delete database records.
- Do not expose PostgreSQL port 5432 or backend port 5000 publicly.