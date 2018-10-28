---
layout: post
title: "Intro to Docker"
date: 2018-10-28 18:20:05
image: 'http://patcody.io/dist-sys-practice/assets/img/docker.png'
description: 'This post discusses the high-level justification for using Docker, as well as an intro to using it.'
category: 'containers'
tags:
twitter_text:
introduction: This post discusses the high-level justification for using Docker, as well as an intro to using it.
---

This post discusses the high-level justification for using Docker, as well as an intro to using it.

## Why Docker? (10 minutes)

- According to the video creator, Docker is a **massive** shift in infrastructure, on par with the mainframe to PC movement and baremetal to virtualization
- Massively simplifies the "Deployment Matrix" of all of the different locations that all of the different pieces of an application are deployed- local
desktops, data centers, a production cluster, etc.
- Docker allows for a single environment to be packaged and pushed to all of these locations
- Docker frees up time that was originally spent on infrastructure maintence 

## DevOps Docker Beginner Guide (30 minutes)

### Hello World Example:

- When running `docker container run hello-world`, Docker looks for the `hello-world` container, (on first run) does not find it, and downloads it from Docker Hub
- Container vs. VM: VMs are a "hardware" abstration, while containers are for "application" abstraction
- `docker image pull <image-name>` downloads an image from the specified Docker registry (Docker Store by default)
- `docker image ls` lists docker images

### Images and Instances
- `docker container run <container-name> <command>` runs the specifed container and the specified command, then exits the container
- For an interactive shell, run `docker run -it <container-name> /bin/sh`
- When you run a container with `docker container run`, it is an **instance** of that image, so created files are not accessible if the image exits
- `docker container start` **starts** a container, which means subsequent commands will be "saved", or run in the same instance


