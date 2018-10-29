---
layout: post
title: "All About Containers"
date: 2018-10-28 21:04:03
image: 'http://patcody.io/dist-sys-practice/assets/img/docker.png'
description: 'In this post, a deep-dive is taken into how containers work and how they differ from VMs. Practical applications are explored through docker.'
category: 'containers'
tags:
twitter_text:
introduction: In this post, a deep-dive is taken into how containers work and how they differ from VMs. Practical applications are explored through docker.
---

In this post, a deep-dive is taken into how containers work and how they differ from VMs. Practical applications are explored through docker.

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

## Lab: Intro to Docker (40 minutes)

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

## Lab: Doing More with Docker Images (30 minutes)

- `docker container diff` allows for viewing changes to a container
- `docker image commit` saves changes made to an image (e.g. when installing new packages)
- Created a dockerfile that installs Node and then runs a JS file
  - `COPY` allows files to be copied from a local directory to somewhere in the container
  - `WORKDIR` is the container startup folder
- In the changed version of the image, some layers in the container didn't have to be downloaded, we already had them in cache
- `docker image inspect` allows viewing of the different layers
  - Alpine only has one layer
  - Custom image has multiple
- Each layer is immutable

## Video: VMs Vs. Containers Deep Dive (10 minutes)

- Myth that containers are always smaller than VMs- not necessarily true
  - VMs have application, user-space stuff for OS (things like package mananger, etc), and the kernel
  - Containers have the application and user-space
  - If it's a big application with lots of user-space requirements, then a container can be many GBs, comparable to a VM
- Security
  - A VM is very secure- incredibly hard to escape not only kernel + EFI, but ALSO x86 it's running on
  - A container is as secure as the _kernel it is running on_- because it shares the kernel with the host OS, it becomes the weak point in the system
  - This is difficult, but not as impossible as breaking out of a VM
- Boot time
  - VM has 2 parts- 1) System check and 2) startup process
  - A container only really has one part- starting the process, which takes as long as a VM
  - As a result, a container has less to do so its faster
