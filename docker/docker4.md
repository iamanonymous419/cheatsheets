# Docker CLI Cheatsheet

This cheatsheet provides a comprehensive list of commonly used Docker commands organized by category.

## Table of Contents
- [Docker Basics](#docker-basics)
- [Container Management](#container-management)
- [Image Management](#image-management)
- [Docker Build](#docker-build)
- [Docker Compose](#docker-compose)
- [Docker Network](#docker-network)
- [Docker Volumes](#docker-volumes)
- [Docker Registry](#docker-registry)
- [Docker System](#docker-system)
- [Docker Logs & Debugging](#docker-logs--debugging)
- [Docker Security](#docker-security)
- [Docker Advanced](#docker-advanced)

## Docker Basics

### Installation & Version
```bash
# Check Docker version
docker --version
docker version  # More detailed version info

# Check Docker system info
docker info
```

### Basic Commands
```bash
# Run a container
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

# Basic run examples
docker run hello-world  # Run hello-world container
docker run -it ubuntu bash  # Run Ubuntu with interactive terminal
docker run -d nginx  # Run Nginx in detached mode (background)

# Help command
docker --help
docker COMMAND --help  # Help for specific command
```

## Container Management

### Running Containers
```bash
# Run container with various options
docker run -it node:latest  # Run interactively with terminal
docker run -d nginx  # Run in detached mode
docker run --name my-container nginx  # Assign a name
docker run -p 8080:80 nginx  # Port mapping (host:container)
docker run -e KEY=VALUE nginx  # Set environment variables
docker run --rm nginx  # Auto-remove container when it exits
docker run -it --init node  # Use an init process
docker run -itd ubuntu  # Interactive, terminal, and detached mode
```

### Container Lifecycle
```bash
# Start, stop, restart containers
docker start CONTAINER
docker stop CONTAINER
docker restart CONTAINER
docker pause CONTAINER
docker unpause CONTAINER

# Kill a container (sends SIGKILL)
docker kill CONTAINER

# Remove a container
docker rm CONTAINER
docker rm -f CONTAINER  # Force remove running container

# Remove all stopped containers
docker container prune

# Run command in a running container
docker exec CONTAINER COMMAND
docker exec -it CONTAINER bash  # Interactive terminal
```

### List Containers
```bash
# List running containers
docker ps
docker container ls

# List all containers (including stopped)
docker ps -a
docker container ls -a

# List containers with size
docker ps -as
```

## Image Management

### Basic Image Commands
```bash
# List images
docker images
docker image ls
docker image ls -a  # Include intermediate images

# Pull an image
docker pull IMAGE[:TAG]
docker pull node:18  # Specific tag
docker pull node:latest  # Latest tag

# Remove image(s)
docker rmi IMAGE
docker image rm IMAGE
docker rmi -f IMAGE  # Force remove
docker image prune  # Remove unused images
docker image prune -a  # Remove all unused images
```

### Image Information
```bash
# Image details
docker inspect IMAGE

# Image history
docker history IMAGE

# Search Docker Hub for images
docker search TERM
```

## Docker Build

### Building Images
```bash
# Build an image
docker build -t NAME:TAG PATH
docker build -t myapp:1.0 .  # Build in current directory

# Build with build arguments
docker build --build-arg KEY=VALUE -t myapp .

# Build without using cache
docker build --no-cache -t myapp .

# Build from specific Dockerfile
docker build -f Dockerfile.dev -t myapp-dev .
```

### Tagging
```bash
# Tag an image
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
docker tag myapp:latest username/myapp:latest
```

## Docker Compose

### Basic Compose Commands
```bash
# Start services
docker-compose up
docker compose up  # (new Docker Compose V2 syntax)

# Start in detached mode
docker-compose up -d

# Stop services
docker-compose down
docker compose down

# Stop services and remove volumes
docker-compose down -v

# Build services
docker-compose build
docker compose build

# Pull service images
docker-compose pull
```

### Other Compose Commands
```bash
# List containers
docker-compose ps

# View logs
docker-compose logs
docker-compose logs -f  # Follow log output

# Run a command in a service
docker-compose exec SERVICE COMMAND
docker-compose exec web bash

# Scale service instances
docker-compose up -d --scale SERVICE=NUM
```

## Docker Network

### Network Management
```bash
# List networks
docker network ls

# Create a network
docker network create NETWORK
docker network create -d bridge my-bridge  # Specify driver
docker network create -d host my-host  # Host network
docker network create --subnet=192.168.0.0/16 my-subnet  # Custom subnet

# Inspect network
docker network inspect NETWORK

# Connect container to network
docker network connect NETWORK CONTAINER

# Disconnect container from network
docker network disconnect NETWORK CONTAINER

# Remove network
docker network rm NETWORK
docker network prune  # Remove all unused networks
```

### Container Networking
```bash
# Run container with specific network
docker run --network=NETWORK IMAGE
docker run --network=host nginx  # Use host networking
docker run --network=none nginx  # No networking

# Create container with hostname
docker run --name db --network my-net --hostname database mysql
```

## Docker Volumes

### Volume Management
```bash
# List volumes
docker volume ls

# Create a volume
docker volume create VOLUME

# Inspect volume
docker volume inspect VOLUME

# Remove volume
docker volume rm VOLUME
docker volume prune  # Remove all unused volumes
```

### Using Volumes with Containers
```bash
# Run container with a volume
docker run -v VOLUME:/path/in/container IMAGE
docker run -v my-data:/var/lib/mysql mysql

# Run with bind-mount (local directory)
docker run -v /host/path:/container/path IMAGE
docker run -v $(pwd):/app node

# Named volumes with docker run
docker run -v my-volume:/app/data nginx

# Read-only volumes
docker run -v my-volume:/app/data:ro nginx

# Run with tmpfs (memory filesystem)
docker run --tmpfs /app/temp nginx

# Run with specified volume driver
docker run -v volume-name:/path --volume-driver=local IMAGE
```

### Advanced Volume Options
```bash
# Create a volume with custom driver and options
docker volume create --driver local \
  --opt type=none \
  --opt device=/host/path \
  --opt o=bind my-volume

# Backup a volume
docker run --rm -v my-volume:/source -v $(pwd):/backup alpine \
  tar -czf /backup/my-volume-backup.tar.gz -C /source .
```

## Docker Registry

### Docker Hub
```bash
# Login to Docker Hub
docker login
docker login -u USERNAME

# Logout from Docker Hub
docker logout

# Push image to Docker Hub
docker push USERNAME/IMAGE[:TAG]

# Pull image from Docker Hub
docker pull USERNAME/IMAGE[:TAG]
```

### Private Registry
```bash
# Login to private registry
docker login REGISTRY_URL

# Push to private registry
docker push REGISTRY_URL/IMAGE[:TAG]

# Pull from private registry
docker pull REGISTRY_URL/IMAGE[:TAG]
```

## Docker System

### System Information
```bash
# Display system-wide information
docker info

# Display Docker disk usage
docker system df

# Show Docker events
docker events
docker events --since '1h'  # Events from the last hour
```

### System Maintenance
```bash
# Remove unused data
docker system prune  # Remove stopped containers, unused networks and images
docker system prune -a  # Remove all unused images, not just dangling ones
docker system prune -a --volumes  # Also remove volumes

# Clean up container logs
truncate -s 0 $(docker inspect --format='{{.LogPath}}' CONTAINER)
```

## Docker Logs & Debugging

### Logs
```bash
# View container logs
docker logs CONTAINER
docker logs -f CONTAINER  # Follow log output
docker logs --tail 100 CONTAINER  # Last 100 lines
docker logs --since 2h CONTAINER  # Logs from last 2 hours

# View logs with timestamps
docker logs -t CONTAINER
```

### Debugging
```bash
# Get container info
docker inspect CONTAINER

# Display container stats
docker stats
docker stats CONTAINER  # For specific container

# Get processes in container
docker top CONTAINER

# Attach to a running container
docker attach CONTAINER

# Copy files between container and host
docker cp CONTAINER:/path/to/file /host/path  # Container to host
docker cp /host/path CONTAINER:/path/to/file  # Host to container
```

## Docker Security

### Security Commands
```bash
# Run container with security options
docker run --security-opt seccomp=profile.json nginx
docker run --security-opt apparmor=profile nginx
docker run --cap-drop ALL --cap-add NET_BIND_SERVICE nginx

# User permissions
docker run -u 1000 nginx  # Run as user with UID 1000
docker run -u 1000:1000 nginx  # Run as user:group with UID:GID 1000:1000

# Add user to docker group (allows non-root to run docker)
sudo usermod -aG docker $USER
```

## Docker Advanced

### Health Checks
```bash
# Add health check when running
docker run --health-cmd="curl -f http://localhost || exit 1" \
  --health-interval=5s nginx
```

### Resource Constraints
```bash
# Memory limits
docker run --memory="512m" nginx
docker run --memory="1g" --memory-swap="2g" nginx

# CPU limits
docker run --cpus=0.5 nginx  # Half of a CPU
docker run --cpus=2 nginx  # 2 CPUs
docker run --cpu-shares=512 nginx  # Relative to other containers
```

### Docker Scout
```bash
# Scan an image for vulnerabilities
docker scout quickview IMAGE
docker scout cves IMAGE  # Common Vulnerabilities and Exposures
```

### Miscellaneous
```bash
# Initialize a Docker project
docker init

# Create a swarm
docker swarm init

# Generate a Compose file from container
docker container ls -a --format '{{.Names}}' | xargs -I {} \
  sh -c 'docker inspect {} > {}.json'
```