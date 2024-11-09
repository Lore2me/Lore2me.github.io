---
layout: post
title: Setup static IP-Adress on raspberry pi
date: 2024-11-09 12:50 +0100
categories: [Raspberry Pi, Networking]
tags: [static ip]
description: This is a guide on how to setup a static IP-Adress on a Raspberry Pi.
---
# Setup static IP-Adress on Raspberry Pi

## Pre-requisites
- A Raspberry Pi
- A computer with SSH access to the Raspberry Pi
- Already connected to the Raspberry Pi via SSH

## Step 1: Manipulate /etc/network/interfaces file
```shell
sudo nano /etc/network/interfaces
```

## Step 2: Change the file to look like this
Add following lines to the file, replacing the placeholders -> * with your network configuration:

```shell
auto eth0
iface eth0 inet static
        address *.*.*.*
        netmask *.*.*.*
        gateway *.*.*.*
        dns-nameservers *.*.*.*
```

## Step 3: Restart the raspberry pi

```shell
sudo reboot
```

## Step 4: Verify the changes
```shell
ifconfig eth0
```
or
```shell
ip addr show eth0
```

## Side note
I used a Raspberry Pi 4 Model B with Raspberry Pi OS (64-bit) for this guide. The steps should be similar for other models and operating systems.
