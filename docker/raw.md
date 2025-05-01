docker run -it node:latest = this command run node latest and -it stands for interact 
docker container ls = for list all container all running containers 
docker container ls -a = for list all container containers 
docker start containerName/containerId = for start the container 
docker stop containerName/containerId = for stop the container 
docker exec containerName/containerId commad = for run the command in docker container 
docker exec -it containerName/containerId commad = for run the command in docker container to multiple command 
docker images or docker image ls or docker image ls -a = for list all images 
docker pull node = for pull node image locally 
docker run -it -p 3000:3000 containerName/containerId commad = this is for port expose and port mapping 
docker run -it -p 3000:3000 -e key = value containerName/containerId =  commad for environment variable passing 
docker build -t imageName pathOfDockerfile = for create a docker image to run 
docker has layer caching 
docker has docker login commad for login in localhost
publisb to docker hub 
docker build -t username/containerName pathName = this for create a docker container 
docker push username/containerName = for push this container in docker hub 
docker image tag Name:latest username/Name:latest = to tag the created image 
Docker-compose.yml 
Create a file called docker-compose.yml/yaml 
docker compose up = this run the docker-compose 
docker compose down = this down the docker-compose 
docker compose up -d = to use this on detached mode 
Docker networking 
docker network inspect networkName = for inspect network container 
docker network ls = for check locally able network driver
 docker run -it --network=host containerName = for give access to local machine 
docker network create -d bridge networkName = for create custom network in local machine
docker network connect name1 name 2 = for connect two network or container 
you can use --name name for this container name 
Docker Volumne 
docker run -it -v yourLocalStorage:containeStroage imageName = this will create a volumne in Localdevice
docker volume create volumeName = to create the volume  
docker run -it -v volumneName/my node bash = for data test local storage 
Tagging in docker 
use docker tag my:v1 username/my:1 = to tag images 
argument in docker build 
Docker build --build-arg key=name -t project  . 
Aws
sudo usermod -aG docker $USER = to add coker as sudo
newgrp docker 
sudo usermod -aG docker jenkins = to jenkins to use docker
sudo systemctl restart jenkins && newgrp docker = for new changes
sudo adduser --disabled-password --gecos "" jenkins = new jenkins user in worker node 
sudo usermod -aG docker jenkins
sudo systemctl restart docker = add Jenkins to use docker 
sudo chmod 666 /var/run/docker.sock = giving permission
sudo -u jenkins docker ps = test working or not 



Docker use containerD 
docker ps means running container 
docker build -it name:tag dockerfilePath to build image with tags 
CMD can be overwritten but ENTRYPOINT not 
ENTEYPOINT always run 
Docker logs containerId = to check logs of project 
docker attach containerId = to check live logs of project 
docker exec -it containerId bash = to work with container 
docker run -itd ubuntu = for continuous run single time code 
docker network create Name -d bridge/host to create network 
docker ls -a = to locate kill container 
docker run --name mysql --network NETWORKNAME mysql = for give network explicit and give containe a host name by --name 
docker restart containerId = to resart docker containerId 
docker create volume mysqlName = to create volume 
docker inspect mysqlName = to check path of volume 
docker run -v my-data:/var/lib/mysql mysql = to store data 
docker run -v loca-lPsth:/var/lib/mysql mysql = to store local 
docker volume create --driver local --opt type=none --opt device=/usr/lib/data --opt o=bind data = a data locate at /usr/lib/data 
docker init = is used to get readymade docker project to use 
docker scout = is used to check error and scan the image 
docker scout quickview IMAGE-NAME = to scan a image 
docker scout cves IMAGE-NAME = to get error 
docker network rm containerId = to delete network 
to connect backend with database in docker it should me same network like addilfy 
docker image tag Name:latest username/Name:latest = to tag the created image 



docker run node = to run node 
docker run -it node = to interact with docker 
code dot for open in vs code in a floder 
Create a Dockerfile 
docker build -t myapp dot 
docker run -p 3000:9000 myapp
COPY . /home/app/
.dockerignore
docker build -t username/projectName . 
docker push username/projectName
docker run -it -p 3000:9000 username/projectName
docker-compose.yml 
docker-compose up
docker-compose down
docker ps 



use docker ps for running container 
use docker pull node for pull a images 
use docker run node and docker run -it node to use images 
docker run --name my-redis -d -p 6379:6379 redis this commad for create a container from image 
docker exec -it my-redis redis-cli  this commad to interact with container files 
docker stop my-redis for stop docker container 
docker rm my-redis for delete docker container 
Use docker images to get list of all images 
use docker start anonymous to start a stop container 
use docker restart anonymous to restart the container 
docker ps -a for all container running Or not running
docker build -t node for build images for dockerfile 
docker rmi node to remove docker images 
docker volume create my_volume for create a volume
docker run -d -v my_volume:/path/in/container my_image 
this above commad create a volumne with container
docker volume rm my_volume for remove volume 
docker volume inspect my_volume for inspect volume
docker volume ls list all volume that are create 
docker image ls to list all docker image 
docker container ls for list all container 
docker push username/appname for push docker container in docker hub 
docker build -t username/appname for create a docker container 
docker run username/app -p 40:3000 for localhost device port 
docker-compose build for create a docker container to use 
docker-compose up for start the container 
docker-compose stop to stop the container 
docker stop containernaem to force stop the container. 
docker rm name for remove container 
docker rmi imageName for delete images 
docker-compose up -d for run docker container for short time means for development