

# **Docker CLI Cheatsheet**

This cheatsheet covers all the important Docker commands categorized for better understanding.

---

## **1. Docker Basics**

### Run Docker Images
```bash
docker run node                    # Run a Node container
docker run -it node                # Run interactively with a Node container
docker run -it ubuntu              # Run an Ubuntu container interactively
docker run -it --name my-container node  # Assign a name to your container
```

### Interactive Mode
```bash
-it                                # Interactive terminal (stdin and TTY enabled)
```

### Expose & Map Ports
```bash
docker run -it -p 3000:3000 node   # Expose container port to host port
docker run -p 3000:9000 myapp      # Map 9000 (host) to 3000 (container)
```

### Run with Environment Variables
```bash
docker run -it -e "KEY=value" node
```

---

## **2. Container Management**

### List Containers
```bash
docker container ls                # List running containers
docker container ls -a            # List all containers (including stopped)
```

### Start, Stop, Restart, and Remove Containers
```bash
docker start <container_name_or_id>
docker stop <container_name_or_id>
docker restart <container_name_or_id>
docker rm <container_name_or_id>  # Remove a container
```

### Attach & Exec into Containers
```bash
docker exec -it <container_id> bash     # Run bash inside container
docker exec -it <container_id> <cmd>    # Run any command
docker attach <container_id>           # Attach terminal to container
```

### View Container Logs
```bash
docker logs <container_id>
```

---

## **3. Docker Images**

### Image Management
```bash
docker images                         # List images
docker image ls                       # Same as above
docker image ls -a                    # List all images
docker pull node                      # Download latest Node image
docker rmi <image_name>               # Remove image
```

### Build & Tag Images
```bash
docker build -t myapp .               # Build Docker image from Dockerfile
docker build -t username/appname .    # Tag with Docker Hub username
docker tag myapp:latest username/myapp:1.0  # Tag local image
```

### Push to Docker Hub
```bash
docker login                          # Authenticate with Docker Hub
docker push username/appname          # Push image to Docker Hub
```

---

## **4. Docker Volumes**

### Volume Management
```bash
docker volume create my_volume
docker volume ls
docker volume inspect my_volume
docker volume rm my_volume
```

### Use Volume in Container
```bash
docker run -v my_volume:/data my_image
docker run -v /local/path:/container/path my_image
```

---

## **5. Docker Networks**

### Network Management
```bash
docker network ls                        # List available networks
docker network create -d bridge my_net   # Create custom network
docker network inspect my_net            # Inspect network details
docker network connect my_net my_container
```

### Use Host Network
```bash
docker run --network=host my_container
```

---

## **6. Docker Compose**

### Compose File Setup
- Create a file `docker-compose.yml`

```bash
docker-compose up                      # Start services
docker-compose up -d                   # Detached mode
docker-compose down                    # Stop and remove services
docker-compose stop                    # Stop containers
docker-compose build                   # Build images
```

---

## **7. Dockerfile Instructions**

### Basic Dockerfile Commands
```dockerfile
FROM node:18
WORKDIR /home/app/
COPY . .
RUN npm install
CMD ["node", "index.js"]
```

- `.dockerignore` to ignore files during build
- `CMD` can be overridden; `ENTRYPOINT` always runs
- `--build-arg` is used to pass variables to Docker build

```bash
docker build --build-arg key=value -t myapp .
```

---

## **8. Docker with Redis Example**

```bash
docker run --name my-redis -d -p 6379:6379 redis
docker exec -it my-redis redis-cli
docker stop my-redis
docker rm my-redis
```

---

## **9. Docker with AWS / Jenkins**

```bash
sudo usermod -aG docker $USER
newgrp docker
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
sudo systemctl restart docker
sudo chmod 666 /var/run/docker.sock
```

---

## **10. Docker Extras**

### Docker Scout (Security Scanning)
```bash
docker scout quickview <image>
docker scout cves <image>
```

### Initialize Project
```bash
docker init                           # Set up dockerized project quickly
```
