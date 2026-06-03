# Docker Commands Cheat Sheet

---

## Container Management

### List running containers
docker ps
→ Shows only running containers

### List all containers
docker ps -a
→ Shows running + stopped containers

### Stop container
docker stop <container_id>

### Remove container
docker rm <container_id>

### Force remove container
docker rm -f <container_id>
→ Removes running container forcefully

---

## Logs

### View logs
docker logs <container_id>

### Live logs (follow mode)
docker logs -f <container_id>
→ Shows real-time logs

---

## Images

### List images
docker images

### Remove image
docker rmi <image_id>

### Pull image
docker pull nginx
→ Downloads image from Docker Hub

---

## Execute inside container

### Open shell inside container
docker exec -it <container_id> bash

If bash not available:
docker exec -it <container_id> sh

---

## Inspect (Detailed info)

### Inspect container
docker inspect <container_id>

### Inspect image
docker inspect <image_id>

→ Shows full JSON details (network, env, ports, config)

---

## docker run commands

### Basic run with port mapping
docker run -p 8080:8080 <image-name>

→ Maps host port 8080 → container port 8080

---

### Run in background + name + port
docker run -d -p 3000:3000 --name my-app node

Options:
- -d → run in background
- -p → port mapping
- --name → container name

---

## System Cleanup

### Remove stopped containers
docker container prune

### Remove unused images
docker image prune

### Full cleanup (containers + images + volumes)
docker system prune -a

---

## Docker Compose

### Start services
docker compose up

### Start in background
docker compose up -d

### Stop services
docker compose down

---

## Quick Reference

| Task | Command |
|------|--------|
| Run container | docker run |
| List containers | docker ps |
| Logs | docker logs |
| Execute shell | docker exec |
| Stop container | docker stop |
| Remove container | docker rm |
| List images | docker images |
| Pull image | docker pull |
| Compose up | docker compose up |

---

## Most Used Commands

docker run
docker ps
docker logs
docker exec
docker stop
docker rm
docker images
docker pull
docker compose up