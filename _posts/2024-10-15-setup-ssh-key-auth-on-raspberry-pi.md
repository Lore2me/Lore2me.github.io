---
layout: post
title: Setup SSH Key Auth on Raspberry Pi
date: 2024-10-15 10:58 +0200
categories: [SSH, Raspberry Pi, Authentication]
tags: [ssh, key, auth, raspberry pi]
description: This is a guide on how to setup SSH Key Authentication on a Raspberry Pi.
---
# Setup SSH Key Auth on Raspberry Pi
## Pre-requisites
- A Raspberry Pi
- A computer with PUTTY installed

## Step 1: Generate SSH Key Pair
1. Open PUTTYgen
2. Click on "Generate"
3. Move your mouse around the blank area to generate randomness
4. Save the public and private keys

## Step 2: Add Public Key to Raspberry Pi
1. Open PUTTY
2. Connect to your Raspberry Pi
3. Open the file `~/.ssh/authorized_keys`

If the folder does not exist, create it with the following command:
```shell
install -d -m 700 ~/.ssh
```

If the file does not exist, create it with the following command:
```shell
nano ~/.ssh/authorized_keys
```

4. Now copy the public key into the file "authorized_keys" and save it with CTRL + X, Y and ENTER.
5. Make sure the file has the correct permissions:
```shell
sudo chmod 644 ~/.ssh/authorized_keys
sudo chown pi:pi ~/.ssh/authorized_keys
```

## Step 3: Connect to Raspberry Pi with SSH Key
1. Open PUTTY
2. Insert the IP address of your Raspberry Pi
3. Go to "Connection" -> "SSH" -> "Auth" -> "Credentials"
4. Click on "Browse" and select the private key file, matching the public key on the Raspberry Pi
5. Click on "Open" and connect to your Raspberry Pi
6. (If you have set a secret for your private key, you will be asked to enter it now)
7. You are now connected to your Raspberry Pi via SSH with Key Authentication

## Step 4: Disable Password Authentication
1. Open the file `/etc/ssh/sshd_config`
2. Change the following line:
```shell
PasswordAuthentication no
```
3. Save the file and restart the server:
```shell
sudo reboot
```
*Sidenote: Before rebooting, make sure you can still connect to your Raspberry Pi via SSH with Key Authentication.*

## Conclusion
You have successfully set up SSH Key Authentication on your Raspberry Pi. You can now connect to your Raspberry Pi without entering a password.
```
