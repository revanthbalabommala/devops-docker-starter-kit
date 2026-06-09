# Docker Networking

## What is Docker Networking?

Docker networking enables communication between Docker containers, the host machine, and external applications.

By default, a container runs in an isolated environment and cannot be accessed directly from outside unless a port is explicitly exposed and mapped.

If an external application needs to communicate with a Docker container, network access must be configured. Docker provides different network drivers to handle various networking requirements.

---

## Types of Docker Networks

Docker supports multiple network types:

### 1. Bridge Network

* Default network type used by Docker.
* Allows containers on the same host to communicate with each other.
* Provides internal DNS-based service discovery.
* Commonly used for application and database communication.

### 2. Host Network

* The container shares the host machine's network stack.
* No separate container IP address is assigned.
* Offers better performance but less isolation.

### 3. None Network

* Completely disables networking for the container.
* The container cannot communicate with other containers or external systems.

### 4. Overlay Network

* Used for communication between containers running on different Docker hosts.
* Commonly used in Docker Swarm environments.

### 5. Macvlan Network

* Assigns a unique IP address to each container on the physical network.
* Makes containers appear as independent devices on the LAN.

---

## Port Mapping

Port mapping allows a container's internal port to be exposed to the host machine so that external users or applications can access the service running inside the container.

Example:

```bash
docker run -d \
  -p 8080:80 \
  -p 8443:443 \
  nginx
```

In the above example:

```text
Host Port 8080 --> Container Port 80
Host Port 8443 --> Container Port 443
```

A single container can expose multiple ports using multiple `-p` options.

---

## Port Conflict

Two different containers cannot use the same host port simultaneously because the host port is already occupied by the first container.

Example:

```bash
docker run -d --name app1 -p 8080:80 nginx
docker run -d --name app2 -p 8080:80 nginx
```

The second container will fail to start because host port `8080` is already in use.

Correct approach:

```bash
docker run -d --name app1 -p 8080:80 nginx
docker run -d --name app2 -p 8081:80 nginx
```

---

## Checking Container Network Information

### List Running Containers

```bash
docker ps
```

Copy the container name from the output.

---

### Inspect a Container

```bash
docker inspect <container-name>
```

This command returns detailed JSON information about the container, including network settings.

Example:

```bash
docker inspect poc-app5
```

---

### Display Only Network Information

```bash
docker inspect -f '{{json .NetworkSettings.Networks}}' <container-name>
```

Example:

```bash
docker inspect -f '{{json .NetworkSettings.Networks}}' poc-app5
```

Output:

```json
{
  "bridge": {
    "IPAddress": "172.17.0.2"
  }
}
```

This indicates that the container is attached to the `bridge` network.

---

## Listing Available Docker Networks

To view all Docker networks available on the host:

```bash
docker network ls
```

Example:

```text
NETWORK ID     NAME      DRIVER
37d362d17972   bridge    bridge
10683ff29204   host      host
dfa8f453ce5a   none      null
```

---

## Inspecting a Docker Network

To view detailed information about a specific network:

```bash
docker network inspect <network-name>
```

Example:

```bash
docker network inspect bridge
```

This command displays:

* Network configuration
* Connected containers
* Assigned IP addresses
* Driver information

---

## Key Takeaway

Docker containers communicate through Docker networks. The most commonly used network type is the **Bridge Network**, which allows containers to communicate using container names and private IP addresses. To make a container accessible from outside, ports must be published using port mapping (`-p hostPort:containerPort`).