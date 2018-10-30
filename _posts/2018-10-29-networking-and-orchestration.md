---
layout: post
title: "Networking and Orchestration"
date: 2018-10-29 04:49:31
image: 'http://patcody.io/dist-sys-practice/assets/img/docker.png'
description: This post explores networking with Docker, and orchestration with Docker Swarm and Kubernetes.
category: 'containers'
tags:
twitter_text:
introduction: This post explores networking with Docker, and orchestration with Docker Swarm and Kubernetes.
---

This post explores networking with Docker, and orchestration with Docker Swarm and Kubernetes.

## Lab: Docker Networking (45 minutes)

- `docker network <command>` allows for accessing various commands about networking
  - `ls` lists all docker networks
  - `inspect <network>` lists details about the network
- The **bridge** network provides single-host networking (meaning only on the local Docker host)
  - `bridge` package and `brctl show` allow for viewing bridge interfaces
  - **bridge** network is the default for new containers
- In the example we ran a container and pinged the container
- Created a container running NGINX that we can `curl`
  - Mapped port 8080 on the Docker host to port 80 in the container
- New docker swarms can be created by running `docker swarm init` on the manager node and then copying the `docker swarm join` command it outputs
  - `docker node ls` lists all node
  - Docker network is called an _overlay_ network
  - This network doesn't exist (yet) on the second node, it is only connected when needed
  - After downloading a sample service that runs on both, it can be verified that it is running on 2/2 nodes
  - The `overlay` network is now in use on node2
  - The two nodes can ping each other
- When done, the network needs to be cleaned up
  - Need to remove the nodes from the swarm, and remove the network interfaces

## Lab: Swarm Mode Introduction (30 minutes)

- Run `docker swarm init` to create swarm
- Run `docker swarm join <token details>` to join the manager
- A **stack** is a group of services that are deployed together, different components that run in seperate instances
  - Each service can have multiple **tasks**, which are one or more containers
  - This stack is defined either in a Compose file or Dockerfile, and defines each layer
  - This is in a YAML file
  - Build stack with `docker stack deploy --compoose-file=<STACK_FILE>`
  - `docker stack services <strack name>` shows all services running on the stack
  - `docker scale` allows more instances of the stack to be deployed- very useful if something like a web app is overwhelmed with traffic

## Video: Docker Swarm Vs. Kubernetes (5 minutes)

- Swarm allows for container deployment on a cluster
- Kubernetes is orchestration software for Docker
- Docker swarm and Kubernetes are in "competition", they do similar stuff
- Most production applications use kubernetes
- Arguably has more features

## Video: Kubernetes in 5 minutes (5 minutes)

- **Kubernetes** allows for enforcement of "desired state management"
  - Provide cluster config info, and Kubernetes will execute that
- **Worker**: Basically a container host, but it runs the "kubelet" process, this communicates with the Kubernetes Cluster Services node
- Deployyment YAML file
  - A "pod" is the smallest object in this file, you can run one or more containers
    - Specify what containers and ports and such
  - Can specify replicas of a pod, or more pods
- Feed this deployment script to the API and the envrionment will execute it
- If a worker dies, the Kubernetes cluster service will pick a new worker to execute the pod in

## Kubernetes on My Own (30 Minutes)

- Followes tutorial with Minikube, software designed for creating small clusters
- `kubectl` is the command-line interface for controlling kubernetes
- Kubernetes Deployment Controller monitors and self-heals if a node goes down
- `kubectl run` allows for running of an app- this creates a pod
- Pods 
  - A pod is one or more application contianers that all share storage, networking (one IP address), and info on how to run each container
  - Pods run on Nodes
  - Pods have internal cluster IPs, as well as an external Node IP
- Nodes
  - A node is a "worker" in a kubernetes cluster, and it may be either a VM or a physical server
  - Each node runs Kubelet and has a container runtime (like Docker)
  - `kubectl expose` allows for exposing ports on a node
- Kubernetes allows for rolling updates- meaning each pod is updated one at a time so that there is 0 downtime

## Exercise: Orchestration of Docker on EC2 (90 Minutes)

- Created EC2 instance, then created image with docker
- Created additional EC2 instances with that image
- Installed Kubernetes on seperate EC2 host
- Set up kubelet service on each host
- Connected service to main Kubernetes process on the Kubernetes host
