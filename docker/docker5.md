# Docker CLI Cheatsheet

This comprehensive cheatsheet provides an extensive list of Docker commands organized by category, covering everything from basic operations to advanced features.

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
- [Container Resource Management](#container-resource-management)
- [Docker Context](#docker-context)
- [Docker Plugins](#docker-plugins)
- [Docker Config](#docker-config)
- [Docker Secrets](#docker-secrets)
- [Docker Swarm](#docker-swarm)
- [Docker Stacks](#docker-stacks)
- [Docker Services](#docker-services)
- [Docker Healthchecks](#docker-healthchecks)
- [Docker Multistage Builds](#docker-multistage-builds)
- [Docker Scout](#docker-scout)
- [Docker Checkpoint](#docker-checkpoint)
- [Docker Miscellaneous](#docker-miscellaneous)

## Docker Basics

### Installation & Version
```bash
# Check Docker version
docker --version
docker version  # More detailed version info

# Check Docker system info
docker info

# Check Docker CLI help
docker
docker --help
docker COMMAND --help  # Help for specific command
```

### Basic Commands
```bash
# Run a container
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

# Basic run examples
docker run hello-world  # Run hello-world container
docker run -it ubuntu bash  # Run Ubuntu with interactive terminal
docker run -d nginx  # Run Nginx in detached mode (background)
docker run --rm alpine echo "Hello World"  # Run and remove after execution

# Get Docker stats
docker stats
```

### Container Exit Codes
```bash
# Exit codes
# 0: Normal exit (success)
# 1-125: Error exit codes
# 126: Command cannot be executed
# 127: Command not found
# 128+n: Fatal error signal "n"
# 137: Container killed (SIGKILL)
# 143: Container terminated (SIGTERM)
```

## Container Management

### Running Containers
```bash
# Run container with various options
docker run -it node:latest  # Run interactively with terminal
docker run -d nginx  # Run in detached mode
docker run --name my-container nginx  # Assign a name
docker run -p 8080:80 nginx  # Port mapping (host:container)
docker run -p 8080:80 -p 8443:443 nginx  # Multiple port mappings
docker run -P nginx  # Publish all exposed ports to random ports
docker run -e KEY=VALUE nginx  # Set environment variables
docker run -e KEY1=VALUE1 -e KEY2=VALUE2 nginx  # Multiple env variables
docker run --env-file .env nginx  # Load environment variables from file
docker run --rm nginx  # Auto-remove container when it exits
docker run -it --init node  # Use an init process
docker run -itd ubuntu  # Interactive, terminal, and detached mode
docker run --restart=always nginx  # Always restart container
docker run --restart=on-failure:5 nginx  # Restart on failure (max 5 times)
docker run --platform linux/amd64 nginx  # Specify platform
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
docker kill --signal=SIGINT CONTAINER  # Send different signal

# Rename a container
docker rename OLD_NAME NEW_NAME

# Wait for container to exit and return exit code
docker wait CONTAINER

# Remove a container
docker rm CONTAINER
docker rm -f CONTAINER  # Force remove running container
docker rm -v CONTAINER  # Remove associated volumes
docker rm $(docker ps -aq)  # Remove all containers

# Remove all stopped containers
docker container prune
docker container prune --filter "until=24h"  # Remove containers older than 24h

# Run command in a running container
docker exec CONTAINER COMMAND
docker exec -it CONTAINER bash  # Interactive terminal
docker exec -u root CONTAINER bash  # Run as root
docker exec -w /path CONTAINER bash  # Set working directory
docker exec -e VAR=value CONTAINER bash  # Set environment variable
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

# List containers with custom format
docker ps --format "table {{.ID}}\t{{.Names}}\t{{.Status}}"
docker ps --format "{{.Names}}: {{.Status}}"

# List containers with filters
docker ps --filter "status=running"
docker ps --filter "name=web"
docker ps --filter "label=env=production"
docker ps --filter "ancestor=nginx"
docker ps --filter "volume=my-volume"
docker ps --filter "network=my-network"
```

### Container Creation Without Running
```bash
# Create container without starting it
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
docker create --name my-nginx nginx

# Create container with specific entrypoint
docker create --entrypoint "/bin/bash" nginx
```

### Container Update
```bash
# Update container configuration
docker update --memory 512m --cpus 0.5 CONTAINER
docker update --restart=always CONTAINER
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
docker pull --platform linux/amd64 node  # Specific platform
docker pull --all-tags nginx  # Pull all tags

# Remove image(s)
docker rmi IMAGE
docker image rm IMAGE
docker rmi -f IMAGE  # Force remove
docker image prune  # Remove unused images
docker image prune -a  # Remove all unused images
docker image prune --filter "until=24h"  # Remove images older than 24h
```

### Image Information
```bash
# Image details
docker inspect IMAGE
docker image inspect IMAGE

# Image history
docker history IMAGE
docker history --no-trunc IMAGE  # Full commands

# Search Docker Hub for images
docker search TERM
docker search --filter stars=100 nginx  # Filter by stars
docker search --limit 10 nginx  # Limit results
docker search --filter is-official=true nginx  # Official images only
```

### Image Export/Import
```bash
# Save image to tar file
docker save -o filename.tar IMAGE
docker save IMAGE > filename.tar

# Load image from tar file
docker load -i filename.tar
docker load < filename.tar

# Export container filesystem as tar
docker export CONTAINER > container.tar

# Import container filesystem as image
docker import container.tar new-image:tag
```

## Docker Build

### Building Images
```bash
# Build an image
docker build -t NAME:TAG PATH
docker build -t myapp:1.0 .  # Build in current directory
docker build -t myapp:1.0 -t myapp:latest .  # Multiple tags

# Build with build arguments
docker build --build-arg KEY=VALUE -t myapp .
docker build --build-arg HTTP_PROXY=http://proxy.example.com -t myapp .

# Build with labels
docker build --label "com.example.vendor=ACME" -t myapp .

# Build without using cache
docker build --no-cache -t myapp .

# Build with specific Dockerfile
docker build -f Dockerfile.dev -t myapp-dev .
docker build -f /path/to/Dockerfile -t myapp .

# Build with specific target stage
docker build --target development -t myapp:dev .

# Build with network settings
docker build --network=host -t myapp .

# Build with specific platform
docker build --platform linux/amd64 -t myapp .

# Build with build context from stdin
docker build -t myapp - < Dockerfile
```

### Tagging
```bash
# Tag an image
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
docker tag myapp:latest username/myapp:latest
docker tag myapp:latest myapp:v1.2.3
docker tag myapp:latest localhost:5000/myapp:latest  # For private registry
```

### Image Layers
```bash
# View image layers
docker history IMAGE
docker history --no-trunc IMAGE  # Full commands
```

## Docker Compose

### Basic Compose Commands
```bash
# Start services
docker-compose up
docker compose up  # (new Docker Compose V2 syntax)

# Start in detached mode
docker-compose up -d

# Start specific services
docker-compose up service1 service2

# Stop services
docker-compose down
docker compose down

# Stop services and remove volumes
docker-compose down -v

# Stop services and remove images
docker-compose down --rmi all

# Build services
docker-compose build
docker compose build

# Build specific services
docker-compose build service1 service2

# Build with no cache
docker-compose build --no-cache

# Pull service images
docker-compose pull
docker-compose pull service1

# Push service images
docker-compose push
```

### Other Compose Commands
```bash
# List running services
docker-compose ps

# List all services
docker-compose ps -a

# View logs
docker-compose logs
docker-compose logs -f  # Follow log output
docker-compose logs --tail=100  # Last 100 lines
docker-compose logs service1  # Logs for specific service

# Run a command in a service
docker-compose exec SERVICE COMMAND
docker-compose exec web bash
docker-compose exec -T web npm test  # Non-interactive

# Run a one-off command
docker-compose run SERVICE COMMAND
docker-compose run --rm web npm install

# Restart services
docker-compose restart
docker-compose restart service1

# Scale service instances
docker-compose up -d --scale SERVICE=NUM
docker-compose up -d --scale web=3 --scale worker=2

# Check config
docker-compose config
docker-compose config --services  # List services

# List containers
docker-compose ps

# Pause/unpause services
docker-compose pause
docker-compose unpause
```

### Compose File Versions
```bash
# Compose file versions
# v1: Legacy format
# v2: Added network and volume support
# v3: Added deploy options (for Swarm)
# v3.x: Various improvements
```

## Docker Network

### Network Management
```bash
# List networks
docker network ls
docker network ls --filter driver=bridge

# Create a network
docker network create NETWORK
docker network create -d bridge my-bridge  # Specify driver
docker network create -d host my-host  # Host network
docker network create --subnet=192.168.0.0/16 my-subnet  # Custom subnet
docker network create --subnet=192.168.0.0/16 --gateway=192.168.0.1 my-net
docker network create --internal my-internal  # Internal network
docker network create --ipv6 --subnet=2001:db8::/64 my-ipv6  # IPv6 network
docker network create --opt com.docker.network.bridge.name=docker1 my-net  # With options

# Inspect network
docker network inspect NETWORK
docker network inspect --format '{{json .Containers}}' NETWORK

# Connect container to network
docker network connect NETWORK CONTAINER
docker network connect --ip 192.168.0.10 NETWORK CONTAINER  # Static IP
docker network connect --alias db NETWORK CONTAINER  # With alias

# Disconnect container from network
docker network disconnect NETWORK CONTAINER
docker network disconnect -f NETWORK CONTAINER  # Force disconnect

# Remove network
docker network rm NETWORK
docker network rm $(docker network ls -q)  # Remove all networks
docker network prune  # Remove all unused networks
docker network prune --filter "until=24h"  # Remove networks older than 24h
```

### Container Networking
```bash
# Run container with specific network
docker run --network=NETWORK IMAGE
docker run --network=host nginx  # Use host networking
docker run --network=none nginx  # No networking
docker run --network=bridge nginx  # Default bridge network

# Create container with specific IP
docker run --ip 192.168.0.10 --network my-net nginx

# Create container with hostname
docker run --name db --network my-net --hostname database mysql

# Create container with DNS
docker run --dns 8.8.8.8 nginx
docker run --dns-search example.com nginx

# Create container with extra hosts
docker run --add-host=host.docker.internal:host-gateway nginx
docker run --add-host=db:192.168.1.10 nginx

# Create container with MAC address
docker run --mac-address 02:42:ac:11:00:02 nginx
```

## Docker Volumes

### Volume Management
```bash
# List volumes
docker volume ls
docker volume ls --filter "dangling=true"

# Create a volume
docker volume create VOLUME
docker volume create --driver local VOLUME
docker volume create --label env=prod VOLUME

# Inspect volume
docker volume inspect VOLUME
docker volume inspect --format '{{.Mountpoint}}' VOLUME

# Remove volume
docker volume rm VOLUME
docker volume rm $(docker volume ls -q)  # Remove all volumes
docker volume prune  # Remove all unused volumes
docker volume prune --filter "label=env=dev"  # Remove with filter
```

### Using Volumes with Containers
```bash
# Run container with a volume
docker run -v VOLUME:/path/in/container IMAGE
docker run -v my-data:/var/lib/mysql mysql

# Run with bind-mount (local directory)
docker run -v /host/path:/container/path IMAGE
docker run -v $(pwd):/app node
docker run -v /home/user/app:/app:ro node  # Read-only

# Named volumes with docker run
docker run -v my-volume:/app/data nginx

# Anonymous volumes
docker run -v /app/data nginx

# Read-only volumes
docker run -v my-volume:/app/data:ro nginx

# Run with tmpfs (memory filesystem)
docker run --tmpfs /app/temp nginx
docker run --tmpfs /app/temp:rw,size=1g,exec nginx  # With options

# Docker's new volume mount syntax
docker run --mount type=volume,source=my-volume,target=/app/data nginx
docker run --mount type=bind,source=/host/path,target=/app/data nginx
docker run --mount type=tmpfs,target=/app/temp nginx

# Run with specified volume driver
docker run -v volume-name:/path --volume-driver=local IMAGE
docker run --mount type=volume,source=my-volume,volume-driver=local,target=/app/data nginx
```

### Advanced Volume Options
```bash
# Create a volume with custom driver and options
docker volume create --driver local \
  --opt type=none \
  --opt device=/host/path \
  --opt o=bind my-volume

# Create a volume with labels
docker volume create --label env=prod --label app=web my-volume

# Backup a volume
docker run --rm -v my-volume:/source -v $(pwd):/backup alpine \
  tar -czf /backup/my-volume-backup.tar.gz -C /source .

# Restore a volume
docker run --rm -v my-volume:/dest -v $(pwd):/backup alpine \
  tar -xzf /backup/my-volume-backup.tar.gz -C /dest
```

## Docker Registry

### Docker Hub
```bash
# Login to Docker Hub
docker login
docker login -u USERNAME
docker login -u USERNAME -p PASSWORD  # Not recommended for security

# Logout from Docker Hub
docker logout

# Push image to Docker Hub
docker push USERNAME/IMAGE[:TAG]
docker push username/myapp:latest

# Pull image from Docker Hub
docker pull USERNAME/IMAGE[:TAG]
docker pull username/myapp:latest

# Search Docker Hub
docker search IMAGE
docker search --filter stars=10 nginx
```

### Private Registry
```bash
# Login to private registry
docker login REGISTRY_URL
docker login registry.example.com

# Push to private registry
docker push REGISTRY_URL/IMAGE[:TAG]
docker push registry.example.com/myapp:latest

# Pull from private registry
docker pull REGISTRY_URL/IMAGE[:TAG]
docker pull registry.example.com/myapp:latest

# Run a local registry
docker run -d -p 5000:5000 --name registry registry:2
docker run -d -p 5000:5000 --name registry -v /path/to/data:/var/lib/registry registry:2

# Push to local registry
docker tag myapp:latest localhost:5000/myapp:latest
docker push localhost:5000/myapp:latest

# Pull from local registry
docker pull localhost:5000/myapp:latest
```

## Docker System

### System Information
```bash
# Display system-wide information
docker info
docker info --format '{{json .}}'

# Display Docker disk usage
docker system df
docker system df -v  # Verbose

# Show Docker events
docker events
docker events --since '1h'  # Events from the last hour
docker events --until '2023-01-01'  # Events until date
docker events --filter 'container=my-container'  # Filter by container
docker events --filter 'event=start'  # Filter by event type
```

### System Maintenance
```bash
# Remove unused data
docker system prune  # Remove stopped containers, unused networks and images
docker system prune -a  # Remove all unused images, not just dangling ones
docker system prune -a --volumes  # Also remove volumes
docker system prune -f  # Force remove without confirmation

# Disk usage
docker system df
docker system df -v  # Verbose

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
docker logs --until 2023-01-01T12:00:00 CONTAINER  # Logs until date/time

# View logs with timestamps
docker logs -t CONTAINER

# View logs with details
docker logs --details CONTAINER
```

### Debugging
```bash
# Get container info
docker inspect CONTAINER
docker inspect --format '{{json .State}}' CONTAINER  # Get specific section
docker inspect --format '{{.NetworkSettings.IPAddress}}' CONTAINER  # Get IP address

# Display container stats
docker stats
docker stats CONTAINER  # For specific container
docker stats --no-stream CONTAINER  # Without continuous output
docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}"  # Custom format

# Get processes in container
docker top CONTAINER
docker top CONTAINER aux  # With specific ps format

# Attach to a running container
docker attach CONTAINER
docker attach --sig-proxy=false CONTAINER  # Don't proxy signals

# Copy files between container and host
docker cp CONTAINER:/path/to/file /host/path  # Container to host
docker cp /host/path CONTAINER:/path/to/file  # Host to container
docker cp CONTAINER1:/path CONTAINER2:/path  # Between containers

# Diff container changes
docker diff CONTAINER  # Show changes to container filesystem
```

## Docker Security

### Security Commands
```bash
# Run container with security options
docker run --security-opt seccomp=profile.json nginx
docker run --security-opt apparmor=profile nginx
docker run --security-opt no-new-privileges nginx
docker run --security-opt label=level:s0:c100,c200 nginx  # SELinux

# Capability management
docker run --cap-drop ALL nginx  # Drop all capabilities
docker run --cap-drop ALL --cap-add NET_BIND_SERVICE nginx  # Add specific capability
docker run --privileged nginx  # Run with full privileges

# User permissions
docker run -u 1000 nginx  # Run as user with UID 1000
docker run -u 1000:1000 nginx  # Run as user:group with UID:GID 1000:1000
docker run -u nobody nginx  # Run as nobody user
docker run --user nobody nginx  # Alternative syntax

# Add user to docker group (allows non-root to run docker)
sudo usermod -aG docker $USER
newgrp docker  # Apply group changes without logout

# Add jenkins user to docker group
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins

# Docker socket permissions
sudo chmod 666 /var/run/docker.sock  # Allow non-root users to access Docker socket
```

### Content Trust
```bash
# Enable Docker Content Trust (DCT)
export DOCKER_CONTENT_TRUST=1

# Sign image when pushing
docker push USERNAME/IMAGE:TAG

# Disable DCT for a single command
DOCKER_CONTENT_TRUST=0 docker pull IMAGE:TAG
```

## Container Resource Management

### Memory Limits
```bash
# Set memory limits
docker run --memory="512m" nginx
docker run --memory="1g" --memory-swap="2g" nginx  # Memory + swap
docker run --memory-reservation="256m" nginx  # Soft limit
docker run --kernel-memory="100m" nginx  # Kernel memory limit
docker run --oom-kill-disable nginx  # Disable OOM Killer
```

### CPU Limits
```bash
# Set CPU limits
docker run --cpus=0.5 nginx  # Half of a CPU
docker run --cpus=2 nginx  # 2 CPUs
docker run --cpu-shares=512 nginx  # Relative to other containers
docker run --cpu-period=100000 --cpu-quota=50000 nginx  # Advanced CPU configuration
docker run --cpuset-cpus="0,1" nginx  # Specific CPU cores
docker run --cpuset-mems="0,1" nginx  # Specific memory nodes (NUMA)
```

### Block I/O Limits
```bash
# Set block I/O limits
docker run --blkio-weight=500 nginx  # Weight (default 500, range 10-1000)
docker run --device-read-bps=/dev/sda:1mb nginx  # Limit read rate
docker run --device-write-bps=/dev/sda:1mb nginx  # Limit write rate
docker run --device-read-iops=/dev/sda:1000 nginx  # Limit read IOPS
docker run --device-write-iops=/dev/sda:1000 nginx  # Limit write IOPS
```

### Pids Limit
```bash
# Limit number of processes
docker run --pids-limit=100 nginx
```

### Update Resource Limits
```bash
# Update resource limits for running container
docker update --cpus=1 CONTAINER
docker update --memory=1G CONTAINER
docker update --memory=1G --memory-swap=2G CONTAINER
```

## Docker Context

### Context Management
```bash
# List contexts
docker context ls

# Create a new context
docker context create my-context --docker "host=ssh://user@host"
docker context create my-context --docker "host=tcp://192.168.99.100:2376"

# Use a context
docker context use my-context

# Inspect context
docker context inspect my-context

# Remove context
docker context rm my-context
```

## Docker Plugins

### Plugin Management
```bash
# List plugins
docker plugin ls

# Install a plugin
docker plugin install PLUGIN[:TAG]
docker plugin install grafana/loki-docker-driver:latest

# Enable/disable a plugin
docker plugin enable PLUGIN
docker plugin disable PLUGIN

# Inspect plugin
docker plugin inspect PLUGIN

# Remove plugin
docker plugin rm PLUGIN
```

## Docker Config

### Config Management
```bash
# Create a config
docker config create my-config config.json

# List configs
docker config ls

# Inspect config
docker config inspect my-config

# Remove config
docker config rm my-config
```

### Using Configs with Services
```bash
# Create service with config
docker service create --name my-service \
  --config source=my-config,target=/path/in/container,mode=0440 \
  nginx
```

## Docker Secrets

### Secret Management
```bash
# Create a secret
docker secret create my-secret secret.txt
echo "my secret data" | docker secret create my-secret -

# List secrets
docker secret ls

# Inspect secret
docker secret inspect my-secret

# Remove secret
docker secret rm my-secret
```

### Using Secrets with Services
```bash
# Create service with secret
docker service create --name my-service \
  --secret source=my-secret,target=/path/in/container \
  nginx
```

## Docker Swarm

### Swarm Initialization
```bash
# Initialize a swarm
docker swarm init
docker swarm init --advertise-addr 192.168.1.100

# Get join token for worker
docker swarm join-token worker

# Get join token for manager
docker swarm join-token manager
```

### Swarm Management
```bash
# List nodes
docker node ls

# Inspect node
docker node inspect NODE
docker node inspect self

# Update node status
docker node update --availability drain NODE  # Drain node
docker node update --availability active NODE  # Activate node

# Promote/demote node
docker node promote NODE  # Worker to manager
docker node demote NODE  # Manager to worker

# Remove node
docker node rm NODE
docker node rm --force NODE
```

### Swarm Services
```bash
# List services
docker service ls

# Create a service
docker service create --name my-service nginx
docker service create --name my-service --replicas 3 nginx

# Update service
docker service update --image nginx:1.19 my-service
docker service update --replicas 5 my-service

# Scale service
docker service scale my-service=5

# Inspect service
docker service inspect my-service
docker service inspect --pretty my-service

# Service logs
docker service logs my-service
docker service logs -f my-service  # Follow

# Remove service
docker service rm my-service
```

## Docker Stacks

### Stack Management
```bash
# Deploy a stack
docker stack deploy -c docker-compose.yml my-stack
docker stack deploy --prune -c docker-compose.yml my-stack

# List stacks
docker stack ls

# List services in a stack
docker stack services my-stack

# List tasks in a stack
docker stack ps my-stack

# Remove a stack
docker stack rm my-stack
```

## Docker Services

### Service Commands
```bash
# Create a service
docker service create --name my-service nginx
docker service create --name my-service --replicas 3 nginx
docker service create --name my-service --mode global nginx  # One per node

# Update service
docker service update --image nginx:1.19 my-service
docker service update --replicas 5 my-service
docker service update --limit-cpu 0.5 my-service
docker service update --limit-memory 512M my-service
docker service update --update-parallelism 2 my-service  # Parallel updates
docker service update --update-delay 10s my-service  # Delay between updates
docker service update --rollback-parallelism 2 my-service  # Rollback config

# Scale service
docker service scale my-service=5
docker service scale service1=3 service2=5  # Scale multiple services

# Inspect service
docker service inspect my-service
docker service inspect --pretty my-service

# Service logs
docker service logs my-service
docker service logs -f my-service  # Follow

# Remove service
docker service rm my-service
```

## Docker Healthchecks

### Healthcheck Commands
```bash
# Run with healthcheck
docker run --health-cmd="curl -f http://localhost/ || exit 1" \
  --health-interval=5s \
  --health-retries=3 \
  --health-timeout=2s \
  --health-start-period=15s \
  nginx

# Disable healthcheck
docker run --no-healthcheck nginx
```

### Healthcheck in Dockerfile
```bash
# Healthcheck in Dockerfile
HEALTHCHECK --interval=5s --timeout=3s \
  CMD curl -f http://localhost/ || exit 1
```

## Docker Multistage Builds

### Multistage Build Examples
```bash
# Basic multistage build
FROM node:14 AS builder
WORKDIR /app
COPY . .
RUN npm ci && npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html

# Multiple stages
FROM golang:1.16 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

FROM alpine:latest
COPY --from=builder /app/myapp /usr/local/bin/
CMD ["myapp"]
```

## Docker Scout

### Scout Commands
```bash
# Initialize Scout
docker scout init

# Scan an image
docker scout quickview IMAGE
docker scout cves IMAGE  # Common Vulnerabilities and Exposures
docker scout recommendations IMAGE  # Get recommendations

# Compare images
docker scout compare IMAGE1 IMAGE2
```

## Docker Checkpoint

### Checkpoint Commands
```bash
# Create a checkpoint
docker checkpoint create CONTAINER CHECKPOINT_NAME

# List checkpoints
docker checkpoint ls CONTAINER

# Start container from checkpoint
docker start --checkpoint CHECKPOINT_NAME CONTAINER

# Remove checkpoint
docker checkpoint rm CONTAINER CHECKPOINT_NAME
```

## Docker Miscellaneous

### Docker Init
```bash
# Initialize Docker project
docker init
docker init --namespace myapp
docker init --platform java
```

### Docker Commit
```bash
# Create image from container
docker commit CONTAINER IMAGE[:TAG]
docker commit -a "Author" -m "Commit message" CONTAINER IMAGE[:TAG]
```

### Docker Custom Formatting
```bash
# Custom formatting with Go templates
docker ps --format "table {{.ID}}\t{{.Names}}\t{{.Status}}"
docker inspect --format '{{.NetworkSettings.IPAddress}}' CONTAINER
docker image ls --format "{{.Repository}}:{{.Tag}}"
```

### Docker Housekeeping
```bash
# Clean up everything
docker system prune -a --volumes

# Clean up individual components
docker container prune  # Containers
docker image prune -a  # Images
docker volume prune  # Volumes
docker network prune  # Networks
```

### Docker Compose Variants
```bash
# Docker Compose v1 (legacy)
docker-compose up

# Docker Compose v2 (integrated)
docker compose up

# Run Compose in production
docker compose -f docker-compose.yml -f docker-compose.prod.yml up
```

### Docker Limits
```bash
# Default limits
# Max containers per host: Limited by system resources
# Default container memory: No limit
# Default container CPU: No limit
# Container name length: 242 characters
# Path length: 242 characters
# Dockerfile size: Limited by system resources
# Layer size: Limited by system resources
```

### Docker daemon configuration
```bash
# Configure Docker daemon
# Edit /etc/docker/daemon.json
{
  "default-address-pools": [
    {"base": "172.30.0.0/16", "size": 24}
  ],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}

# Restart Docker daemon
sudo systemctl restart docker
```

### Docker CLI Environment Variables
```bash
# Common Docker environment variables
DOCKER_HOST=tcp://127.0.0.1:2375  # Connect to remote Docker daemon
DOCKER_TLS_VERIFY=1  # Use TLS
DOCKER_CERT_PATH=~/.docker/certs  # Path to TLS certificates
DOCKER_CONTENT_TRUST=1  # Enable content trust
DOCKER_BUILDKIT=1  # Enable BuildKit
DOCKER_CLI_EXPERIMENTAL=enabled  # Enable experimental features
DOCKER_CONTEXT=my-context  # Use specific context
DOCKER_COMPOSE_CONVERT_WINDOWS_PATHS=1  # Convert Windows paths
```

### Docker Troubleshooting
```bash
# Check Docker logs
sudo journalctl -u docker

# Check Docker daemon status
sudo systemctl status docker

# Check Docker info
docker info

# Check Docker disk usage
docker system df -v

# Check Docker events
docker events

# Check Docker network
docker network inspect bridge

# Container diagnostics
docker inspect CONTAINER
docker stats CONTAINER
docker top CONTAINER
docker logs CONTAINER
```