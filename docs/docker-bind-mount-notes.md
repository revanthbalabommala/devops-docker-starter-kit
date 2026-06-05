# Docker Bind Mount Notes (Mounting Local Directory)

---

# 1. What is Bind Mount?

A bind mount allows you to mount a **local directory from your machine (Mac/Windows/Linux)** directly into a Docker container.
Unlike Docker volumes, the data is stored on your host machine.

---

# 2. Why use Bind Mount?

- See files directly on your Mac  
- Easy development workflow  
- Live sync between host and container  
- Useful for logs, code changes, uploads  

---

# 3. Example Use Case (Spring Boot Logs)

### Local directory:

/Users/revanthbalabommala/Downloads/poc/logs

### Container directory:

/app/logs


---

# 4. Run Container with Bind Mount

```bash id="bind2"
docker run -d \
  --name poc-app \
  -p 8080:8080 \
  -v /Users/revanthbalabommala/Downloads/poc/logs:/app/logs \
  poc:0.9.1

#5. Verify on Mac - ls /Users/revanthbalabommala/Downloads/poc/logs

#6. Verify inside Container

docker exec -it poc-app bash
ls -l /app/logs

Docker Run Example:

docker run -d \
  --name poc-app5 \
  -p 8080:8080 \
  -v /Users/revanthbalabommala/Downloads:/app/logs \
  poc:0.9.5

Docker Volume Commands (Quick Reference):

Create a volume: docker volume create my-data-volume
List all volumes: docker volume ls
Inspect a volume: docker volume inspect my-data-volume
Remove all unused volumes: docker volume prune  