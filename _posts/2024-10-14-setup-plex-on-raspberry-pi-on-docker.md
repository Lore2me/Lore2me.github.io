---
layout: post
title: Setup Plex on Raspberry Pi on Docker
date: 2024-10-14 16:52 +0200
categories: [Plex, Docker]
tags: [plex, raspberry pi, docker]
description: How to setup Plex on a Raspberry Pi using Docker
---
# Setup Plex on Raspberry Pi on Docker
Plex is a media server that allows you to stream your media to any device.
It is a great tool to have if you have a lot of media and want to access it from anywhere.
In this guide, I will show you how to setup Plex Media Server on a Raspberry Pi using Docker.

## Prerequisites
Before we get started, you will need a Raspberry Pi with Raspbian installed.

## Install Docker
The first thing you need to do is install Docker on your Raspberry Pi.

But before you can install it, be sure that no other version is already installed on your system.

This command removes all the packages that are related to Docker and could get you in trouble if you have them already installed:
```bash
 for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

Setup the Docker apt repository:

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "bookworm") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Now install Docker:

```bash
 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verify that Docker is installed correctly:

```bash
 sudo docker run hello-world
```
If everything is installed correctly, you should see Hello World printed in your terminal.

## Install Docker Compose
Docker Compose is a tool that allows you to define and run multi-container Docker applications.

To install Docker Compose, run the following commands:

```bash
sudo apt install docker-compose
```

## Setup Plex on Docker
Now that you have Docker installed on your Raspberry Pi, you can setup Plex using Docker Compose.

Create a new directory for your Plex configuration:

```bash
mkdir ~/plex
cd ~/plex
```

Create a new file called docker-compose.yml and add the following configuration:
```bash
nano docker-compose.yml
```
Enter following content:
```yaml
version: '3'
services:
  plex:
    image: ghcr.io/linuxserver/plex
    container_name: plex
    environment:
      - PUID=1000
      - PGID=1000
      - VERSION=docker
      - PLEX_CLAIM=claim-xxxxxxxxxxxx
    volumes:
      - ~/plex/config:/config
      - ~/plex/data:/data
      - ~/plex/transcode:/transcode
    ports:
      - "32400:32400"
      - "3005:3005"
      - "8324:8324"
      - "32469:32469"
      - "1900:1900/udp"
      - "32410:32410/udp"
      - "32412:32412/udp"
      - "32413:32413/udp"
      - "32414:32414/udp"
    restart: unless-stopped
```
Replace `claim-xxxxxxxxxxxx` with your Plex claim token. You can get the claim token from [Plex](https://www.plex.tv/claim/).

There is a YAML Validator to check if the yaml file is correct: [YAML Validator](https://codebeautify.org/yaml-validator/)

Save the file and exit the editor.

Now you can start the Plex container using Docker Compose:

```bash
docker-compose up
```
*Optional: run the container in the background:*
```bash
docker-compose up -d
```

Plex should now be running on your Raspberry Pi.

## Data outside of the container
If you want to store your Plex data outside of the container, you can do so by declare the volumes in the docker-compose.yml file.

Add in the example above the following lines:
```yaml
    volumes:
      - ...
      - /mywishdirecotry/media:/media
```

You need to be sure that the directory exists on your Raspberry Pi and that the user running the container has the necessary permissions to access the directory.

To grant the necessary permissions, run the following commands:
```bash
sudo chown -R 1000:1000 /mywishdirecotry/media
sudo chmod -R 755 /mywishdirecotry/media
```

# Configurate Plex
To access the Plex web interface, open a web browser and go to http://your-raspberry-pi-ip:32400/web.

Source: [sunfounder.com](https://www.sunfounder.com/blogs/news/raspberry-pi-plex-server)
