# Docker Commands

## 1. Check Docker Version

bash
docker --version


## 2. Check Docker Information

bash
sudo docker info


## 3. Check Running Containers

bash
sudo docker ps


## 4. Check All Containers

bash
sudo docker ps -a


## 5. List Docker Images

bash
sudo docker images


## 6. Pull Docker Image

bash
sudo docker pull nginx:alpine


## 7. Run a Docker Container

bash
sudo docker run -d -p 8080:80 --name test-nginx nginx:alpine


## 8. Stop Container

bash
sudo docker stop test-nginx


## 9. Start Container

bash
sudo docker start test-nginx


## 10. Restart Container

bash
sudo docker restart test-nginx


## 11. View Container Logs

bash
sudo docker logs my-frontend-container
sudo docker logs my-python-container
sudo docker logs my_postgres


## 12. Follow Container Logs

bash
sudo docker logs -f my-python-container


## 13. Access Container Shell

bash
sudo docker exec -it my-frontend-container sh


## 14. Execute Command Inside Container

bash
sudo docker exec my_postgres psql -U admin -d studentdb


## 15. Inspect Container

bash
sudo docker inspect my-frontend-container


## 16. Remove Container

bash
sudo docker rm test-nginx


## 17. List Docker Networks

bash
sudo docker network ls


## 18. Inspect Docker Network

bash
sudo docker network inspect mynetwork


## 19. List Docker Volumes

bash
sudo docker volume ls


## 20. Inspect Docker Volume

bash
sudo docker volume inspect pgdata


## 21. Check Docker Disk Usage

bash
sudo docker system df


## 22. Remove Unused Docker Images

bash
sudo docker image prune


## 23. Remove Unused Docker Containers

```bash
sudo