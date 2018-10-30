---
layout: post
title: "Breaking Up a Monolithic Application"
date: 2018-10-29 15:44:21
image: 'http://patcody.io/dist-sys-practice/assets/img/aws.png'
description:
category: 'containers'
tags:
twitter_text:
introduction: Utilizing a variety of AWS Services, this post explores how to convert a monolithic application to use several microservices instead. 
---

Utilizing a variety of AWS Services, this post explores how to convert a monolithic application to use several microservices instead. 

## Why Microservices?

- A monolithic application is hard to scale if there are many different components that are all entangled with each other
- A microservices architecture means each component is its own seperate service, meaning it is easy to swap out services if maintence or updates are required

## Setup

- Installed docker and the awscli
- Cloned the github repo
- Ran the normal application to test
![Running Monolith](http://patcody.io/dist-sys-practice/assets/img/monolithic_running.png)
- With some difficulty due to AWS over-engineering, set up awscli access by creating IAM user
- Create `api` container registry on AWS
![ECR Creation](http://patcody.io/dist-sys-practice/assets/img/ecr_creation.png)

## Containerizing

- Initialize Docker daemon
- build docker container
- Push to the ECR from setup
![Pushed Containers](http://patcody.io/dist-sys-practice/assets/img/pushed_image.png)

## Deploying the Monolith

- Takes the container with everything coupled together and deploys it to EC2 instances
- Create Cloud Formation stack
- Need to create service task for application to run
- Then create application load balancer to handle incoming traffic

## Breaking the Monolith

- First need to provision repos for each container needed by the application
  - This app results in 4 total
- Build each of the containers in the part 3 folder
- Push those built containers to the provisioned ECR repos

## Deploying the Microservices

- Created 3 task microservices, each with its own task definition
- Can use the load balancer from the monolith stage
- Added new rules to account for each new microservice
- In `ecs` menu, creating actual services for each microservice- this is how they are "deployed"
- In the load balancer, switch traffic to use the microservices
