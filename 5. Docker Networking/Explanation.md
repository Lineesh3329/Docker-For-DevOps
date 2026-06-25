# Docker Networking

## What is Docker Networking?

Docker Networking is a feature that enables Docker containers to communicate with each other, the host machine, and external networks in a secure and isolated manner.

It allows containers running on the same or different hosts to exchange data using Docker-managed networks.

---

### Why Docker Networking?

By default, containers run in isolated environments and cannot communicate with one another directly.

Docker Networking solves this by providing networking mechanisms that enable containers to:

- Communicate with other containers
- Connect to the host machine
- Access external networks and the internet
- Isolate application traffic for security
- Build multi-container applications

### Before Docker Networking

Without Docker Networking:

- Containers could not communicate easily.
- Applications consisting of multiple services (e.g., frontend, backend, database) could not interact efficiently.
- Manual IP address management was required.
- Communication between containers was complex and error-prone.
- Scaling containerized applications became difficult.

### The Solution:

Docker introduced **Networking** to provide secure and efficient communication between containers.

Using Docker Networks, containers can:

1. Discover each other automatically
2. Communicate using container names
3. Access external services
4. Isolate different applications using separate networks

---

### How Docker Networking Works

When a container is created, Docker can connect it to one or more networks.

Each container receives:

- A unique IP address
- A network interface
- DNS resolution within the Docker network

Docker automatically routes traffic between containers connected to the same network.

### Docker Networking Workflow

```text
        Internet
            │
            ▼
     Docker Host
            │
    Docker Network
   ┌────────┼────────┐
   ▼        ▼        ▼
Container A Container B Container C
```

---

### Key Features

- Container-to-container communication
- Automatic DNS resolution
- Network isolation
- Port mapping
- Multiple network support
- Secure communication between containers

---
## Types of Docker Networks

Docker provides different network drivers to support various communication requirements between containers and external systems.

| Network Type | Description | Best Use Case |
|--------------|-------------|---------------|
| **Bridge** | The default network for containers running on the same Docker host. | Communication between containers on a single host. |
| **Host** | Shares the host machine's network stack with the container. | High-performance applications requiring direct host networking. |
| **None** | Disables all networking for the container. | Completely isolated or secure workloads. |
| **Overlay** | Connects containers running across multiple Docker hosts. | Docker Swarm and distributed applications. |
| **Macvlan** | Assigns a unique MAC and IP address to each container, making it appear as a physical device on the network. | Legacy applications and direct network integration. |


- **Bridge** → Connects containers on the same Docker host.
- **Host** → Uses the host machine's network directly.
- **None** → No network connectivity.
- **Overlay** → Connects containers across multiple Docker hosts.
- **Macvlan** → Assigns a unique IP and MAC address to each container.
---

### Key Takeaway

- Docker Networking enables containers to communicate securely with each other, the host machine, and external networks, making it essential for building scalable and production-ready containerized applications.

## Custom Bridge Network

### What is a Custom Bridge Network?

A Custom Bridge Network is a user-defined Docker network that allows containers on the same Docker host to communicate securely using **container names** instead of IP addresses.

Unlike the default bridge network, a custom bridge network provides automatic DNS resolution, better isolation, and easier container communication.

---

### Why Use a Custom Bridge Network?

- Enables communication using container names
- Provides automatic DNS resolution
- Better network isolation
- Easier management of multi-container applications
- More secure than the default bridge network

---

### How It Works

```text
                Docker Host
                     │
         ┌────────────────────┐
         │ Custom Bridge      │
         │    Network         │
         └────────────────────┘
            │            │
            ▼            ▼
      Container A   Container B
      (frontend)    (backend)
```

Containers connected to the same custom bridge network can communicate using their container names.

---

````markdown
# Custom Bridge Network Example

## Step 1: Create a Custom Bridge Network
docker network create my-network

## Step 2: Verify the Network
docker network ls

## Step 3: Run Containers on the Network

docker run -d --name frontend --network my-network nginx
docker run -d --name backend --network my-network httpd

## Step 4: Test Container Communication

Access the frontend container:

docker exec -it frontend sh

Ping the backend container using its container name:

ping backend

Docker automatically resolves the container name (`backend`) to its IP address.

## Step 5: Inspect the Network

docker network inspect my-network

## Step 6: Disconnect a Container from the Network

docker network disconnect my-network backend

Verify the network:

docker network inspect my-network

## Step 7: Reconnect the Container

docker network connect my-network backend

Verify again:

docker network inspect my-network

## Step 8: Remove Containers

docker rm -f frontend backend

## Step 9: Remove the Network

docker network rm my-network
`````
------------------------



### Default Bridge vs Custom Bridge

| Feature | Default Bridge | Custom Bridge |
|---------|----------------|---------------|
| Created Automatically | ✅ Yes | ❌ No |
| Automatic DNS Resolution | ❌ No | ✅ Yes |
| Container Name Communication | ❌ Limited | ✅ Yes |
| Network Isolation | Basic | Better |
| Best Use Case | Simple containers | Multi-container applications |

---

### Benefits
- Automatic DNS resolution
- Easy container-to-container communication
- Better security and isolation
- Ideal for microservices and multi-container applications

### Networking Best Practices
- Use Custom Bridge Networks
- Don't use the default bridge in production
- Use DNS instead of IP addresses
- Use separate networks for different applications
- Expose only required ports

### Key Point
- A Custom Bridge Network is the recommended network type for containers running on the same Docker host.
- It provides automatic service discovery, secure communication, and simplifies networking by allowing containers to communicate using their names instead of IP addresses.

------------------------------------

## Docker Networking Commands

### 1. Network Management

| Command | Description | Example |
|---------|-------------|---------|
| `docker network ls` | List all Docker networks | `docker network ls` |
| `docker network create` | Create a new network | `docker network create my-network` |
| `docker network inspect` | View detailed network information | `docker network inspect my-network` |
| `docker network rm` | Remove a network | `docker network rm my-network` |
| `docker network prune` | Remove all unused networks | `docker network prune` |

### 2. Container Network Management

| Command | Description | Example |
|---------|-------------|---------|
| `docker network connect` | Connect a container to a network | `docker network connect my-network web` |
| `docker network disconnect` | Disconnect a container from a network | `docker network disconnect my-network web` |

### 3. Running Containers on a Network

| Command | Description | Example |
|---------|-------------|---------|
| `docker run --network` | Run a container on a specific network | `docker run -d --name web --network my-network nginx` |
| `docker run -p` | Map a host port to a container port | `docker run -d -p 8080:80 nginx` |


### 4. Container Communication

| Command | Description | Example |
|---------|-------------|---------|
| `docker exec` | Access a running container | `docker exec -it web bash` |
| `ping` | Test connectivity between containers | `ping backend` |
| `curl` | Test HTTP connectivity | `curl http://backend:8080` |


### 5. Container Information

| Command | Description | Example |
|---------|-------------|---------|
| `docker ps` | List running containers | `docker ps` |
| `docker inspect` | View container details including network settings | `docker inspect web` |


### 6. DNS & Port Verification

| Command | Description | Example |
|---------|-------------|---------|
| `docker port` | View mapped ports | `docker port web` |
| `hostname -i` | Display the container's IP address | `hostname -i` |
| `ip addr` | Show network interfaces inside the container | `ip addr` |

-----------------
### Conclusion

Docker Networking is a fundamental feature that enables secure and efficient communication between containers, the host machine, and external networks. By using different network drivers, custom bridge networks, DNS-based name resolution, and port mapping, Docker simplifies the deployment of scalable, isolated, and production-ready applications. Understanding Docker Networking is essential for building reliable multi-container and microservices-based applications.

---
