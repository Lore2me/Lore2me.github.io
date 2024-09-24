---
layout: post
title: Docker and Docker Compose
date: 2024-06-14 15:31 +0200
categories: [Knowledge, Docker]
tags: [docker, docker-compose]
description: In today’s world, every developer should know about Docker and Docker Compose. So, let’s start with the basics.
---
## Docker
Docker is a platform for developing, shipping, and running applications in containers. It enables developers to separate their applications from the infrastructure so they can deliver software quickly.
The propably most important feature of Docker is
that it allows you
to package an application with all of its dependencies into a standardized unit for software development.  
The great benefit of this is that you can run and test the application on any machine that has Docker installed,
regardless of the customized settings that machine might have that could differ from the machine
used for writing and testing the code.
And many bugs caused by differences between the development and production environments are all eliminated by Docker by default.  
Also is every version of each library and code is defined and stored in the Docker image, so you can always go back to a previous version of the application if needed.

### Dockerfile
A Dockerfile is a text document
that contains all the commands a user could call on the command line to assemble an image.  

Using `docker init` starts a wizard, where you can create a new Dockerfile in the current directory.
```shell
docker init
```

After completion, the Dockerfile and the docker compose file will be created in the current directory.

Now you can build the Docker image with the following command:
```shell 
docker build -t my-docker-image .
```
My-docker-image is the name of the image,
and the dot at the end of the command specifies the current directory as the build context.
The name should be changed to the name of the image you want to create.

To run the Docker image, you can use the following command:
```shell
docker run -d -p 8080:80 my-docker-image:latest
```
The -d flag runs the container in detached mode,
and the -p flag maps port 80 in the container to port 8080 on the host machine.
my-docker-image is the name of the image you want to run.
Latest is the tag of the image you want to run.
If you don't specify a tag, Docker will use the latest tag by default.
If you want to use a specific version of the image, you write the version number instead of latest.

To show all Images, you can use the following command:
```shell
docker images -a
```

To remove a image, you can use the following command:
```shell
docker rmi my-docker-image:latest
```
my-docker-image is the name of the image you want to remove.

To show all running containers, you can use the following command:
```shell
docker ps
```

To show used ressourced per Container, you can use the following command:
```shell
docker stats
```

## Docker Compose
Docker Compose is a tool for defining and running multi-container Docker applications.
With Compose, you use a YAML file to configure your application’s services.
Then, with a single command, you create and start all the services from your configuration.

After you created the docker-compose file, you can start the application with the following command:
```shell
docker-compose up
```
For a less detailed startup, you can use the following command:
```shell
docker-compose up -d
```
To stop the application, you can use the following command:
```shell
docker-compose down
```

### Docker Compose File
A docker-compose file is a YAML file that defines the services, networks, and volumes for a Docker application.
(Be aware that YAML is not officially defined in genereal)

```yaml
services:
  urlshortener-app:
    image: urlshortener:latest
    ports:
      - 8080:8081
```
This is an example of a docker-compose file of a Spring Boot application.
It defines a service called urlshortener-app that uses the urlshortener image with the latest tag.
It also maps port 8081 in the container to port 8080 on the host machine.

#### Multiple Services
You can define multiple services in a docker-compose file.
The spring boot application and the database are defined as separate services in the following example:
```yaml
services:
  urlshortener-app:
    image: urlshortener:latest
    ports:
      - 8080:8081
    depends_on:
      - urlshortener-database

  urlshortener-database:
    image: mysql:lts
    restart: always
    volumes:
      - url-database:/var/lib/mysql
    ports:
      - 3306:3306

volumes:
  url-database:
```
This example defines two services: urlshortener-app and urlshortener-database.
The urlshortener-app service uses the urlshortener image with the latest tag and maps port 8081 in the container to port 8080 on the host machine.
The urlshortener-database service uses the mysql image with the lts tag and maps port 3306 in the container to port 3306 on the host machine.
It also creates a volume called url-database to persist the database data.
If you don't do this, the data will be lost when the container is stopped.

In this example the urlshortener-app service depends on the urlshortener-database service, so the database will be started before the application.
In this example the communication between the services is not defined,
so the application won't be able to connect to the database.
This will be covered in a future post.

## Docker on Windows
To install Docker on Windows, you can use the following link:
[Docker for Windows](https://docs.docker.com/docker-for-windows/install/)

The reccomended way to install Docker on Windows is to use the Docker Desktop for Windows Installer and WSL 2.
WSL 2 is a new version of the Windows Subsystem for Linux that is optimized for Docker Desktop for Windows.
I tried it myself, and it works great for my purposes.

## Conclusion
Docker and Docker Compose are essential tools for every developer.
They enable you
to package your application with all of its dependencies into a standardized unit for software development.
This allows you to run and test the application on any machine that has Docker installed,
regardless of the customized settings that machine might have that could differ from the machine
used for writing and testing the code.
And many bugs caused by differences between the development and production environments are all eliminated by Docker by default.
Also is every version of each library and code is defined and stored in the Docker image, so you can always go back to a previous version of the application if needed.
Docker Compose is a tool for defining and running multi-container Docker applications.
With Compose, you use a YAML file to configure your application’s services.
Then, with a single command, you create and start all the services from your configuration.
This is a great way to start your application with all the services you need in one command.  

I hope you enjoyed this post and leave a comment if you have any questions.
