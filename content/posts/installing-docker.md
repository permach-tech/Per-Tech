+++
date = '2025-09-30T02:57:20Z'
draft = false
title = 'Docker and Docker Compose Installation on Ubuntu'
featuredImage = '/img/banners/docker.png'
featuredImagePreview = "/img/banners/docker.png"
tags = ["Containers", "Linux"]
categories = ["Development"]
summary = "A quick guide to get you started with Docker on Ubuntu."

toc = true
comments = true
  enable = true
lightgallery = false
license = ""
+++

## Introduction
I am not going to mince words on a Docker introduction. If you are curious about learning more about Docker, I recommend checking out the [official Docker documentation](https://docs.docker.com/get-started/).
Without further ado, let's get started with installing Docker and Docker Compose on Ubuntu.

## Installation

1. Update your existing list of packages(usually the first step in any installation process):
```bash
sudo apt-get update
```
2. Add official GPG keys for Docker:
```bash
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

3. Set up the stable repository for Docker:
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

4. Install the latest version of Docker:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

5.  Type the command `Docker` and you will see the Docker help output.

6. Get your Docker version:
```bash
docker -v
# or docker --version
```

7. Verify that docker compose was installed correctly:
```bash
docker compose
# You will see the docker compose help output
```

## Using Docker without sudo
```bash
sudo usermod -aG docker $USER
```
Log out and log back in so that your group membership is re-evaluated.

## Optional Steps
1. Quick nginx installation to verify:
```bash
docker run -d -p 80:80 --name webserver nginx
```
2. Check Nginx is running:
```bash
docker ps
# You should see the nginx container running
```

## Uninstall Docker
```bash
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```
