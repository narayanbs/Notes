#### Installation
```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install ca-certificates curl gnupg
$ sudo install -m 0755 -d /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

$ sudo chmod a+r /etc/apt/keyrings/docker.gpg

$ echo   "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
"$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

$ sudo apt update
$ sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
$ docker --version
```

**To invoke docker without sudo**
```bash
$ sudo groupadd docker
$ sudo gpasswd -a $USER docker
```

	* Restart docker 
#### Docker Concepts

**Images**
An image is an inert, immutable, file that's essentially a snapshot of a container. Images are created with the build command, Images are stored in a Docker registry such as [registry.hub.docker.com](https://registry.hub.docker.com/).

**Containers**
Containers - Instance of an image. If we start an image, we have a running container of the image. 
To use a programming metaphor, if an image is a class, then a container is an instance of a class

#### Docker Commands

![[Pasted image 20240201213522.png]]


**list of images**
```bash
$ docker images 
```
**list of containers**
```bash
$ docker ps (currently running)
	or
$ docker ps -a (including stopped ones)
```
**Clean up images**
```bash
$ docker rmi <imageid>
	or
$ docker image prune  (remove all unused ones) 
	or
$ docker image prune -a (remove all unused as well as dangling)
```
**clean up containers**
```bash
$ docker rm <containerid1> <containerid2>...
	or
$ docker container prune  (remove all stopped containers)
```
**Search for a new image**
```
$ docker search mysql 
```
**Pull an image**
```bash
$ docker pull mysql:tag   
	or
$ docker pull mysql (if tag is not specified, by default latest will be pulled)
```

**Start a new container from an image**
```bash
$ docker run <options> <imageid or imagetag>

for ex: docker run mysql 
	or
$ docker run -p [port:port] --name=[container_name] --detach  <image_tag_name>

for ex: docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=slayer --name mysql_local -d mysql

```
**Execute a command in a running container**
```bash
$ docker container exec [OPTIONS] CONTAINER COMMAND [ARG...]

for ex: 
$ docker exec -it mysql_local bash
$ docker exec -i mysql_local mysql -uroot -p < init.sql

$ docker exec -it mysql_local bash
> mysql -uroot -p
```
**Stop a container**
```bash
$ docker stop <container_id>
```
**restart a container**
```bash
$ docker restart <container_id>
```

#### Docker Workflow Example

**Mysql using docker**

```bash
$ docker search mysql

$ docker pull mysql

$ docker images

$ docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=slayer --name mysql_local -d mysql

$ docker exec -it mysql_local bash
> mysql -uroot -p

If we are using a sql script 
$ docker exec -i mysql_local mysql -uroot -p < init.sql

check if init.sql has initiated any changes into mysql

```

**MongoDB using docker**
```bash
$ docker search mongo

$ docker pull mongo 

$ docker run -d --name mongodb -p 27017:27017 mongo 

$ docker exec -it mongodb mongosh

$ show databases;
use <db_name>

# Create a mongodb instance and connect against an authentication database

$ docker run -d --network some-network --name some-mongo \
	-e MONGO_INITDB_ROOT_USERNAME=mongoadmin \
	-e MONGO_INITDB_ROOT_PASSWORD=secret \
	mongo

$ docker run -it --rm --network some-network mongo \
	mongosh --host some-mongo \
		-u mongoadmin \
		-p secret \
		--authenticationDatabase admin \
		some-db
> db.getName();
some-db
```


#### Creating Docker Image

* Create an account on docker hub. for ex: `narayan925`
* Let's consider a python project called `auth`
* Create `Dockerfile`, as shown below
  
```bash
FROM python:3.8.18-slim-bullseye

RUN apt-get update \
  && apt-get install -y --no-install-recommends --no-install-suggests \
  build-essential default-libmysqlclient-dev pkg-config \
  && pip install --no-cache-dir --upgrade pip

WORKDIR /app
COPY ./requirements.txt /app
RUN pip install --no-cache-dir --requirement /app/requirements.txt
COPY . /app

EXPOSE 5000

ENV PYTHONUNBUFFERED=1

CMD ["python3", "-u", "server.py"]
	
```
* Execute `docker build .` in the folder containing the `Dockerfile`
* Copy the SHA encoded tag number and tag the image
```bash
$ docker tag <tag_> narayan925/auth:<tag>

for ex:
$ docker tag a23sh92ecsdf237wlk narayan925/gateway:latest
```
* Upload the image to docker hub
```bash
$ docker login -u narayan925

# At the password prompt, enter the personal access token.

# Push image
$ docker push narayan925/auth:latest

```

