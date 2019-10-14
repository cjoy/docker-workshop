# Docker Workshop
This repo contains three sample projects for the [docker workshop](https://www.facebook.com/events/2436141676464170/) I ran on 14th of October, 2019. The slides used for the workshop are [here](https://docs.google.com/presentation/d/1XmV66BpDFzHac93GXBoWxK9-GY30KeK3cXTT4kSh_MI/edit?usp=sharing).

## Hello World!
Check if docker is working.
```
docker run hello-world
```
* This pulls down the hello-world image from docker hub.
* Then it creates & runs a new container, based on that image.


## Run an Ubuntu Container
1. Pull the latest ubuntu image.
```
docker pull ubuntu:latest
```
2. Run a instance of the ubuntu image (ie. the container).
```
docker run -it --name ubuntu-container ubuntu 
```
3. Stop the container.
```
docker container stop ubuntu-container
```
3. Remove the container.
```
docker container rm ubuntu-container
```
5. Remove the image (optional).
```
docker image rm ubuntu:latest
```


## Simple Python Container
This example shows you how to run python script in a docker container.

1. Build the image.
```
docker image build -t python-image ./python-app
```
2. Run the container, using the image we just built.
```
docker container run --name python-container python-image
```
3. Remove the container.
```
docker container rm python-container
```
5. Remove the image (optional).
```
docker image rm python:3
```

## Simple Flask Container
We're now building ontop of the previous example. In this example we run a web server that just returns "Hello World!" when we visit http://localhost:5000

[Flask](https://www.fullstackpython.com/flask.html) is just a python library that allows us to run a web server.

1. Build the image.
```
docker image build -t flask-image ./flask-app
```
2. Run the container, using the image we just build.
```
docker container run -d -p 5000:5000 --name flask-container flask-image
```
* **-d** ~ run as a daemon process.
* **-p HOST_PORT:CONTAINER_PORT** ~ map host & container port

3. Stop the container.
```
docker container stop flask-container
```
4. Remove the container (perhaps so we can create it again??).
```
docker container rm flask-container
```
5. Remove the image (optional).
```
docker image rm flask-image
```

## Flask + MongoDB Containers (Docker Compose)
0. Switch to the directory
```
cd flask-mongodb-app
```
1. Build the containers.
```
docker-compose build
```
2. Run the containers.
```
docker-compose up -d
```
3. Stop the containers.
```
docker-compose down
```


## Misc
### Dockerfile Instructions
```
INSTRUCTION (ARGUMENT)
```
* **ADD** copies the files from a source on the host into the container’s own filesystem at the set destination.
* **RUN** executes command(s) in a new layer and creates a new image.
* **CMD** sets default command and/or parameters, which can be overwritten from command line when docker container runs.
* **ENTRYPOINT** sets a default application to be used every time a container is created with the image.
* **ENV** sets environment variables.
* **EXPOSE** associates a specific port to enable networking between the container and the outside world.
* **FROM** defines the base image used to start the build process.
* **MAINTAINER** defines a full name and email address of the image creator.
* **USER** sets the UID (or username) which is to run the container.
* **VOLUME** is used to enable access from the container to a directory on the host machine.
* **WORKDIR** sets the path where the command, defined with CMD, is to be executed.
* **LABEL** allows you to add a label to your docker image.
