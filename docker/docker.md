Here’s a comprehensive Docker CLI cheatsheet formatted as a `README.md` file, covering all major Docker topics:

---

# Docker CLI Cheatsheet

This cheatsheet covers all essential Docker CLI commands and concepts for managing containers, images, volumes, networks, and Docker Compose.

---

## Table of Contents

- [Docker CLI Cheatsheet](#docker-cli-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Docker Basics](#docker-basics)
  - [Container Commands](#container-commands)
  - [Image Commands](#image-commands)
  - [Dockerfile \& Build](#dockerfile--build)
  - [Environment Variables](#environment-variables)
  - [Volumes](#volumes)
  - [Networks](#networks)
  - [Docker Compose](#docker-compose)
  - [Logs \& Debugging](#logs--debugging)
  - [Docker Hub](#docker-hub)
  - [Docker \& AWS / Jenkins](#docker--aws--jenkins)
  - [Advanced](#advanced)
  - [Common Cleanup](#common-cleanup)
  - [Tip](#tip)

---

## Docker Basics

```bash
docker --version                         # Show Docker version
docker info                              # Show system-wide info
docker login                             # Log in to Docker Hub
docker logout                            # Log out from Docker Hub
docker pull <image>                      # Pull an image
docker run <image>                       # Run container from image
docker run -it <image>                   # Run in interactive terminal
docker ps                                # List running containers
docker ps -a                             # List all containers
```

---

## Container Commands

```bash
docker start <name|id>                   # Start a container
docker stop <name|id>                    # Stop a container
docker restart <name|id>                 # Restart a container
docker rm <name|id>                      # Remove a container
docker exec <name|id> <cmd>              # Run command in container
docker exec -it <name|id> <cmd>          # Run interactive command
docker attach <name|id>                  # Attach to live container
docker logs <name|id>                    # View logs
```

---

## Image Commands

```bash
docker images                            # List images
docker image ls -a                       # List all images
docker build -t <name>:<tag> .           # Build image from Dockerfile
docker rmi <image>                       # Remove image
docker image tag <old> <new>             # Tag an image
docker push <user>/<repo>:<tag>          # Push image to Docker Hub
```

---

## Dockerfile & Build

```bash
docker build -t <imageName> .            # Build from current dir
docker build -t <imageName> <path>       # Build from specific path
docker build --build-arg KEY=value .     # Pass build args
COPY . /app/                             # Copy files into image
.dockerignore                            # Files to ignore while copying
```

---

## Environment Variables

```bash
docker run -e KEY=value <image>          # Pass env variables
docker run --env-file .env <image>       # Load env from file
```

---

## Volumes

```bash
docker volume create <name>              # Create volume
docker volume ls                         # List volumes
docker volume inspect <name>             # Inspect volume
docker volume rm <name>                  # Remove volume
docker run -v <volName>:/path <image>    # Mount volume
docker run -v /host/path:/container/path <image> # Local path
```

---

## Networks

```bash
docker network ls                        # List networks
docker network create -d bridge <name>   # Create custom network
docker network inspect <name>            # Inspect network
docker network rm <name>                 # Remove network
docker network connect <net> <container> # Connect container to network
docker run --network=host <image>        # Use host network
docker run --name <name> --network <net> <image>
```

---

## Docker Compose

```bash
docker-compose build                     # Build services
docker-compose up                        # Start all services
docker-compose up -d                     # Start in detached mode
docker-compose down                      # Stop and remove
docker-compose stop                      # Stop services
```

**docker-compose.yml Example**
```yaml
version: '3'
services:
  app:
    image: node
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    environment:
      - NODE_ENV=development
```

---

## Logs & Debugging

```bash
docker logs <container>                  # Show container logs
docker inspect <container|image|volume>  # Detailed info
docker scout quickview <image>           # Scan image summary
docker scout cves <image>                # Check for vulnerabilities
```

---

## Docker Hub

```bash
docker tag <localName> <user>/<repo>     # Tag for Docker Hub
docker push <user>/<repo>                # Push image
```

---

## Docker & AWS / Jenkins

```bash
sudo usermod -aG docker $USER            # Add user to docker group
newgrp docker                            # Apply new group
sudo usermod -aG docker jenkins          # Give Jenkins docker access
sudo systemctl restart docker            # Restart docker service
sudo chmod 666 /var/run/docker.sock      # Docker socket access
```

---

## Advanced

```bash
docker run -itd ubuntu                   # Run container in detached mode
docker init                              # Get Docker project starter
docker run --name redis -d -p 6379:6379 redis
docker exec -it redis redis-cli          # Redis CLI
docker build -t username/project .       # Tag and build project
docker run -p 3000:9000 username/project
```

---

## Common Cleanup

```bash
docker rm $(docker ps -aq)               # Remove all containers
docker rmi $(docker images -q)           # Remove all images
docker volume prune                      # Remove all unused volumes
docker network prune                     # Remove all unused networks
```

---

## Tip

Use `--name <name>` to easily identify containers, volumes, and networks.

