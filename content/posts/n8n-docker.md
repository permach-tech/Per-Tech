+++
date = '2025-09-28T02:57:20Z'
draft = false
title = 'n8n self-hosted automation at the palm of your hand'
featuredImage = '/img/banners/n8n+docker.png'
featuredImagePreview = "/img/banners/n8n+docker.png"
tags = ["Automation", "Containers"]
enableLastMod = false
categories = ["Development"]
summary = "Automation has never been easier, introducing n8n a powerful self-hosted workflow automation tool"

toc = true
comments = true
  enable = true
lightgallery = false
license = ""
+++

## Introduction
Ever wanted to send emails and alerts? Manage your financial budget? Maybe you want to automatically post to your social media? Or perhaps you just want to send a message to grandma on her birthday so you don't forget. Well, n8n has you covered. n8n is an open-source workflow automation tool that allows you to connect various apps and services to automate tasks and processes. It provides a visual interface where you can create workflows by dragging and dropping nodes, making it easy to set up complex automations without writing code.

<img src="/img/content/power_of_the_sun.jpg" alt="doc-ock" style="width:650px; border-radius:8px; border-radius:8px; display:block; margin-left:auto; margin-right:auto;" />

## Installation
### Installer Docker
You will need [Docker](/posts/installing-docker/)

### Setup
1. I recommend you create a directory to organize your Docker files. For example:<br> `/home/<your_user>/docker/n8n`
```bash
mkdir -p ~/docker/n8n
cd ~/docker/n8n
```

2. Create a `docker-compose.yml` file with the following content:
```bash
# you can use vim, nano, or your favorite text editor
nano docker-compose.yml
```

Paste the following content into the file:
```yaml
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    container_name: n8n
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
	- GENERIC_TIMEZONE= <your-timezone> # Example: America/New_York
	- N8N_SECURE_COOKIE=false
	- NODE_ENV=production
	- N8N_PROTOCOL=https
	- N8N_RUNNERS_ENABLED=true
# - WEBHOOK_URL=https://<your-webhook-url>.com # Enable this option if you want to enable webhooks
# - N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=true # Enable this option if you want to use community packages
    volumes:
      - n8n_data:/home/node/.n8n
    command: start
```

3. Start the container:
```bash
docker-compose up -d
```

4. Check to see the container is running:
```bash
docker ps # should show the n8n container running
```
If you see any errors, you can check the logs with:
```bash
docker logs n8n
```
### Accessing n8n
Open your web browser and navigate to `http://localhost:5678` (or replace 'localhost' with your server's IP address if you're not running it locally). You should see the n8n interface.

If you are using a reverse proxy like Traefik, you can reference the [documentation](https://docs.n8n.io/hosting/installation/server-setups/docker-compose/) to get that configured.

The first time you navigate to your self-hosted n8n instance, you will be greeted with a welcome screen:

<img src="/img/content/n8n_welcome.png" alt="n8n-welcome" style="width:300px; border-radius:8px; display:block; margin-left:auto; margin-right:auto;" />

## Conclusion
Once you are finished with the setup, you are free to start creating your first workflow.
You can create very powerful workflows leveraging AI agents and MCP servers, you can also head over to the [community workflows](https://n8n.io/workflows/?utm_source=n8n_app&utm_medium=template_library&utm_instance=https://n8n.per-tech.org/&utm_n8n_version=1.111.1&utm_awc=1) to get some inspiration.

In another post, I will showcase how to build your first workflow with n8n. Stay tuned! 