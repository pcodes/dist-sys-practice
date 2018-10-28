---
layout: post
title: "Intro to EC2 and S3"
date: 2018-10-26 19:02:14
image: 'http://patcody.io/dist-sys-practice/assets/img/aws.png'
description: A writeup about an intro to using AWS EC2 and S3
category: 'webapps'
tags:
twitter_text:
introduction: Amazon AWS allows for easy hosting of web apps in the cloud, by utilizing a variety of its services. This post explores creating virtual machines using EC2 instances, and cloud storage with S3.
---

Amazon AWS allows for easy hosting of web apps in the cloud, by utilizing a variety of
its services. This post explores creating virtual machines using EC2 instances, and cloud storage with S3.

## Launching a VM (15 minutes)

- EC2 instances have a ton of configurable options, and a big advantage is the "marketplace" of VM images you can choose from
- You also have the ability to create your own image if creating a large number of instances
- After creating an instance, you either pick an existing SSH keypair, or create a new one and download it
- No username/password access

## Intro to S3 (20 minutes)

- S3 allows for object storage in "Buckets", which are similarish to folders
- Each bucket has configurable permissions to allow for different read/write access
- Each item in a bucket _also_ has its own set of permissions
- A **Bucket Policy** allows for bucket-wide permission changes, e.g. setting all the photos in a bucket to be publically accessible
- Policy generator allows for the generation of policy XML
- Buckets can also track versions of files (e.g. Eiffel tower photos)
- By default, only the _latest_ version of a file is publically accessible when the "GetObject" attribute is publically accessible
