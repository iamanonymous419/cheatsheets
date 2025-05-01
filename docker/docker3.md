# Docker Commands Cheat Sheet

## Basic Commands

- **Run a Node container:**
  ```bash
  docker run -it node:latest
  ```

- **List all running containers:**
  ```bash
  docker container ls
  ```

- **List all containers (including stopped ones):**
  ```bash
  docker container ls -a
  ```

- **Start a container:**
  ```bash
  docker start containerName/containerId
  ```

- **Stop a container:**
  ```bash
  docker stop containerName/containerId
  ```

- **Run a command inside a running container:**
  ```bash
  docker exec containerName/containerId command
  ```

- **Run multiple commands inside a container:**
  ```bash
  docker exec -it containerName/containerId command
  ```

- **List all images:**
  ```bash
  docker images
  ```

- **Pull an image locally:**
  ```bash
  docker pull node
  ```

- **Run a container with port mapping:**
  ```bash
  docker run -it -p 3000:3000 containerName/containerId command
  ```

- **Pass environment variables:**
  ```bash
  docker run -it -p 3000:3000 -e key=value containerName/containerId command
  ```

- **Build a Docker image:**
  ```bash
  docker build -t imageName pathOfDockerfile
  ```

- **Log in to Docker Hub:**
  ```bash
  docker login
  ```

- **Tag an image:**
  ```bash
  docker image tag Name:latest username/Name:latest
  ```

## Docker Compose

- **Create a `docker-compose.yml` file** to manage multiple containers.

- **Run Docker Compose:**
  ```bash
  docker compose up
  ```

- **Stop Docker Compose:**
  ```bash
  docker compose down
  ```

- **Run Docker Compose in detached mode:**
  ```bash
  docker compose up -d
  ```

## Docker Networking

- **Inspect a Docker network:**
  ```bash
  docker network inspect networkName
  ```

- **List all Docker networks:**
  ```bash
  docker network ls
  ```

- **Create a custom network:**
  ```bash
  docker network create -d bridge networkName
  ```

- **Connect two containers to the same network:**
  ```bash
  docker network connect networkName containerName
  ```

- **Run a container with network access to the local machine:**
  ```bash
  docker run -it --network=host containerName
  ```

## Docker Volumes

- **Create a volume:**
  ```bash
  docker volume create volumeName
  ```

- **Run a container with a volume mount:**
  ```bash
  docker run -it -v yourLocalStorage:containerStorage imageName
  ```

- **Inspect a volume:**
  ```bash
  docker volume inspect volumeName
  ```

- **List all volumes:**
  ```bash
  docker volume ls
  ```

## Docker Build Arguments

- **Pass build arguments to Docker:**
  ```bash
  docker build --build-arg key=value -t project .
  ```

## AWS Integration

- **Add Docker to a user group (for Jenkins):**
  ```bash
  sudo usermod -aG docker jenkins
  sudo systemctl restart docker
  ```

- **Allow Jenkins to use Docker:**
  ```bash
  sudo systemctl restart jenkins && newgrp docker
  ```

## Docker Logs & Management

- **View logs of a running container:**
  ```bash
  docker logs containerId
  ```

- **Attach to a container to view live logs:**
  ```bash
  docker attach containerId
  ```

- **Work with a container's shell:**
  ```bash
  docker exec -it containerId bash
  ```

- **Restart a container:**
  ```bash
  docker restart containerId
  ```

- **Remove a container:**
  ```bash
  docker rm containerId
  ```

- **Remove an image:**
  ```bash
  docker rmi imageName
  ```

- **Create a volume with a container:**
  ```bash
  docker run -d -v my_volume:/path/in/container my_image
  ```

- **Remove a volume:**
  ```bash
  docker volume rm my_volume
  ```

- **Inspect a volume's path:**
  ```bash
  docker volume inspect my_volume
  ```

## Docker Miscellaneous

- **Build an image with a tag:**
  ```bash
  docker build -t node .
  ```

- **Run a container in the background:**
  ```bash
  docker run -itd ubuntu
  ```

- **Use `.dockerignore` to exclude files from the build context:**
  ```text
  # Example .dockerignore
  node_modules
  *.log
  ```

- **Create a Dockerfile:**
  ```Dockerfile
  COPY . /home/app/
  ```

- **Push an image to Docker Hub:**
  ```bash
  docker push username/projectName
  ```

## Redis Example

- **Run a Redis container:**
  ```bash
  docker run --name my-redis -d -p 6379:6379 redis
  ```

- **Access Redis container:**
  ```bash
  docker exec -it my-redis redis-cli
  ```

- **Stop a container:**
  ```bash
  docker stop my-redis
  ```

- **Delete a container:**
  ```bash
  docker rm my-redis
  ```

## Useful Docker Compose Commands

- **Build Docker Compose containers:**
  ```bash
  docker-compose build
  ```

- **Start Docker Compose containers:**
  ```bash
  docker-compose up
  ```

- **Stop Docker Compose containers:**
  ```bash
  docker-compose stop
  ```

---

This README file can serve as a quick reference for managing Docker containers, images, volumes, and networking.