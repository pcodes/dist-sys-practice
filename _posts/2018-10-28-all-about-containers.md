---
layout: post
title: "All About Containers"
date: 2018-10-28 21:04:03
image: 'http://patcody.io/dist-sys-practice/assets/img/docker.png'
description:
category: ''
tags:
twitter_text:
introduction:
---

## Video: What is a Container? (20 minutes)

- Traditional Linux has seperate processes, and in a container, the process can only see other processes running in that same container
  - This creates a sandbox- each process can run in its own container _on top_ of the Linux OS and not be able to interact with each other
- The lifecycle of a container is usually tied to the lifecycle of the process running within it
  - Container ends when the application ends
- Container images can have a Parent-Child relationship
  - An image can contain a certain set of packages, and the children of that image all have those packages, plus more
  - Example image hierarchy: Scratch OS, Busybox, sshd, application
  - Similar to disk snapshots
- Dockerfile
  - Docker environment in a text file
  - Starts with FROM: (then specify base/parent image)
  - Create containers _from_ a dockerfile
- It is expected that a container is packaged with all of the application dependencies
- When downloading new docker images, the docker host checks to see which images it already has, and it then decides which additional images it needs (this prevents redundancy)
- Docker client can connect to Docker host and push/pull containers, and configure networking and storage

## Video: Containers Vs. VMs (10 minutes)

- Virtual Machines:
  - Run on top of a minimal "OS" or hypervisor, are a bridge between a "traditional" OS and the hardware
  - Hypervisors must provide support for all kinds of different hardware, like different NICs or storage
  - The VM runs on top of this hypervisor and connects to the emulated hardware
  - A VM does not fix the issue of applications having many different dependencies
- Containers:
  - A container is composed of the application and its OS dependencies
  - The OS has whatever drivers it needs to interact with hardware
- There is room to combine the two: have a hypervisor to interact with hardware, a VM to provide emulated hardware, and a container to manage application dependencies

## Lab: Intro to Docker

- `docker container ls --all` lists all downloaded containers
  - A container hostname is the ID displayed in this command
- Passing the `--rm` flag means the container will be deleted when it stops
- Linux containers require a linux kernel on the host OS, so a Windows container can only be run on Windows
- Passing the `--detach` flag keeps the container running but returns the shell to the user, so running `docker container ls` will show that the container is **active**
- There are ways to check the logs of the running container, as well run commands directly on the container
- Dockerfiles
  - `FROM` specifies base image
  - `COPY` copies specific files
  - `EXPOSE` exposes specific ports out of the container
  - `--tag` in `docker image build` allows for a custom name of the image
- `docker container rm` deletes the container
- By binding a container to a directory on the host, files can be changed and reflected **live**, without having to restart the container
- Adding a `--tag` also allows for creating new versions (e.g. linux tweet app)
- After making changes to an image, these changes can be pushed as new images to Docker Hub

## Lab: Doing More with Docker Images

- 
