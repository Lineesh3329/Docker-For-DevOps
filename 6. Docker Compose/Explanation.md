# Docker Compose

Docker Compose is a tool that allows us to define, configure, and manage **multiple Docker containers** using a single YAML configuration file (`docker-compose.yml`).

Instead of running multiple `docker run` commands, Docker Compose enables us to start, stop, and manage all related containers with a single command.

Managing multiple containers individually can be time-consuming and error-prone.

Docker Compose simplifies this process by allowing you to define the entire application stack in a single configuration file.

---

### Before Docker Compose

Before Docker Compose the problem is if developer faces to containerization a huge project:

- Each container had to be started manually.
- Multiple `docker run` commands were required.
- Networking had to be configured manually.
- Volumes needed to be created and mounted individually.
- Environment variables had to be specified for every container.
- Managing multi-container applications was complex.

---

### Problems Solved by Docker Compose

Docker Compose solves several challenges in multi-container environments:

- Starts multiple containers with a single command.
- Automatically creates networks.
- Automatically manages volumes.
- Simplifies service configuration.
- Maintains consistent environments across systems.
- Makes applications easier to deploy and maintain.

---
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/617b53d1-e5c2-493e-abc6-cc79b22b3f35" />

### Docker Compose Architecture Explained

- The `docker-compose.yml` file defines all application services, networks, and volumes.
- Docker Compose reads the configuration when you run `docker compose up`.
- It automatically creates the required networks and volumes.
- It pulls or builds the required Docker images.
- It starts all containers and connects them through the same network.
- The containers communicate with each other using their service names.
- The entire multi-container application is managed using a single configuration file.

### A simple Docker Compose Workflow

          docker-compose.yml
                  │
                  ▼
          docker compose up
                  │
                  ▼
          Create Network ──► Create Volumes ──► Build / Pull Images ──► Start Containers ──► Running Multi-Container Application

---


### Docker Compose File Structure

A Docker Compose file (`docker-compose.yml`) defines all the services, networks, volumes, and configurations required to run a multi-container application.

### Basic Structure

```yaml
services:
  web:
    image: nginx
    ports:
      - "80:80"

  app:
    build: .
    ports:
      - "5000:5000"
    environment:
      - ENV=production
    volumes:
      - app-data:/app
    depends_on:
      - db
    networks:
      - app-network

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - db-data:/var/lib/mysql
    networks:
      - app-network

volumes:
  app-data:
  db-data:

networks:
  app-network:
```

### Docker Compose File Structure Overview

| Section | Purpose | Example |
|---------|---------|---------|
| `services` | Defines all the containers (services) that make up the application. Each service runs as a separate container. | `services:` |
| `image` | Specifies the Docker image to pull and use for a service. | `image: nginx:latest` |
| `build` | Builds a Docker image from a local Dockerfile instead of pulling an existing image. | `build: .` |
| `container_name` | Assigns a custom name to the container instead of an auto-generated one. | `container_name: web` |
| `ports` | Maps a host port to a container port, allowing external access to the application. | `ports: - "8080:80"` |
| `environment` | Sets environment variables required by the application or service. | `environment: MYSQL_ROOT_PASSWORD=root` |
| `env_file` | Loads environment variables from an external `.env` file. | `env_file: .env` |
| `volumes` | Mounts Docker volumes or host directories to persist and share data. | `volumes: - db-data:/var/lib/mysql` |
| `networks` | Connects services to one or more Docker networks for communication. | `networks: - app-network` |
| `depends_on` | Ensures that one service starts before another service. | `depends_on: - db` |
| `restart` | Specifies when Docker should automatically restart the container. | `restart: always` |
| `command` | Overrides the default command defined in the Docker image. | `command: python app.py` |
| `entrypoint` | Overrides the default ENTRYPOINT of the Docker image. | `entrypoint: ["python"]` |
| `healthcheck` | Checks whether the container is healthy and running correctly. | `healthcheck:` |
| `hostname` | Sets a custom hostname for the container. | `hostname: database` |
| `working_dir` | Sets the default working directory inside the container. | `working_dir: /app` |

---

### Docker Compose Commands

These Docker Compose commands are used to build, deploy, manage, monitor, and troubleshoot multi-container applications defined in a `docker-compose.yml` file.

| Category | Command | Description | Example |
|----------|---------|-------------|---------|
| **Project Management** | `docker compose up` | Create and start all services. | `docker compose up` |
| | `docker compose up -d` | Start services in detached mode. | `docker compose up -d` |
| | `docker compose down` | Stop and remove containers and networks. | `docker compose down` |
| | `docker compose start` | Start stopped services. | `docker compose start` |
| | `docker compose stop` | Stop running services. | `docker compose stop` |
| | `docker compose restart` | Restart all services. | `docker compose restart` |
| | `docker compose pause` | Pause all running services. | `docker compose pause` |
| | `docker compose unpause` | Resume paused services. | `docker compose unpause` |
| | `docker compose kill` | Force stop running services. | `docker compose kill` |
| **Build & Images** | `docker compose build` | Build images for all services. | `docker compose build` |
| | `docker compose build <service>` | Build image for a specific service. | `docker compose build web` |
| | `docker compose pull` | Pull images from a registry. | `docker compose pull` |
| | `docker compose push` | Push images to a registry. | `docker compose push` |
| **Monitoring & Logs** | `docker compose ps` | List running service containers. | `docker compose ps` |
| | `docker compose logs` | View logs of all services. | `docker compose logs` |
| | `docker compose logs -f` | Follow logs in real time. | `docker compose logs -f` |
| | `docker compose logs <service>` | View logs of a specific service. | `docker compose logs web` |
| | `docker compose top` | Display running processes. | `docker compose top` |
| | `docker compose events` | View real-time service events. | `docker compose events` |
| **Execute Commands** | `docker compose exec <service> bash` | Open Bash inside a running container. | `docker compose exec web bash` |
| | `docker compose exec <service> sh` | Open Shell inside a running container. | `docker compose exec web sh` |
| | `docker compose run <service>` | Run a one-time command. | `docker compose run web python app.py` |
| **Scaling** | `docker compose up --scale <service>=<count>` | Scale a service to multiple containers. | `docker compose up --scale web=3` |
| **Configuration** | `docker compose config` | Validate and display Compose configuration. | `docker compose config` |
| | `docker compose version` | Display Docker Compose version. | `docker compose version` |
| **Cleanup** | `docker compose down --volumes` | Remove containers, networks, and volumes. | `docker compose down --volumes` |
| | `docker compose down --rmi all` | Remove containers, networks, and images. | `docker compose down --rmi all` |
| | `docker compose rm` | Remove stopped service containers. | `docker compose rm` |
| **File Operations** | `docker compose cp` | Copy files between host and container. | `docker compose cp file.txt web:/app/` |
| **Image Management** | `docker compose images` | List images used by Compose services. | `docker compose images` |
| **Container Status** | `docker compose ls` | List all Compose projects. | `docker compose ls` |
| | `docker compose create` | Create containers without starting them. | `docker compose create` |

---

## Docker Compose vs Kubernetes

### Docker Compose

- Manages multi-container applications on a single machine.
- Simple to set up and use.
- Best suited for development and testing environments.

### Kubernetes

- Orchestrates containers across multiple machines (clusters).
- Provides automatic scaling, self-healing, and load balancing.
- Best suited for production and large-scale applications.

> **Summary:** Docker Compose is ideal for local development and testing, while Kubernetes is designed to deploy, manage, and scale containerized applications in production environments.

## Conclusion

Docker Compose simplifies the deployment and management of multi-container applications by defining all services in a single configuration file. It automates networking, storage, and service management, making application deployment faster, more consistent, and easier to maintain.
