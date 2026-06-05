# Docker + Spring Boot Volumes Cheat Sheet

---

## 1. What is Docker Volume?
A Docker volume is persistent storage outside the container filesystem.  
Data survives container deletion.

---

## 2. Why use volumes?
- Container data is lost when removed  
- Volume keeps data safe and persistent

---

## 3. Spring Boot Configuration

```properties
spring.application.name=poc
logging.file.name=/app/logs/application.log

4. Dockerfile Used

FROM eclipse-temurin:21-jdk

WORKDIR /app

COPY /build/libs/poc-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar"]

5. Create Volume - docker volume create poc-spring-app-logs

6. Run Container with Volume 

docker run -d \
  --name poc-app \
  -p 8080:8080 \
  -v poc-spring-app-logs:/app/logs \
  poc:0.9.1

7. Check Logs

docker logs -f poc-app

8. Verify Inside Container

docker exec -it poc-app bash
ls /app/logs
cat /app/logs/application.log

9. Inspect Volume

docker volume inspect poc-spring-app-logs

10. MacOS Important Note
Docker runs inside a Linux VM on Mac.
/var/lib/docker/... is NOT accessible directly.
You must use a container to inspect volume data.

11. View Volume Data (Correct Approach)

docker run --rm -it \
  -v poc-spring-app-logs:/data \
  alpine sh

Inside container:
ls /data
cat /data/application.log

Docker Volume Commands (Quick Reference):

Create a volume: docker volume create my-data-volume
List all volumes: docker volume ls
Inspect a volume: docker volume inspect my-data-volume
Remove all unused volumes: docker volume prune