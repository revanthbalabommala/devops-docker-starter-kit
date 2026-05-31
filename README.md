# DevOps Docker Starter Kit

A practical, hands-on guide to quickly set up and run applications using Docker and Docker Compose.

## What’s inside

- Java (Spring Boot) Docker setup
- Python (Flask/FastAPI) Docker setup
- Node.js (Express) Docker setup
- Prebuilt Docker Compose templates (DBs, full-stack setups)

## Goal

Help developers quickly:
- Build Docker images
- Run containers
- Use Docker Compose for full environments
- Avoid setup confusion across stacks

## Tech Covered

- Java (Spring Boot)
- Python (Flask / FastAPI)
- Node.js (Express)
- MySQL / Postgres / Redis

## How to use

Each folder contains:
```bash
docker build -t app .
docker run -p 8080:8080 app