---
layout: reads
title:  "Working with docker containers"
date:   2023-06-23
author: "Ahmed Abugharbia"
author_link: "https://twitter.com/aagsec"
---

## Intro

From [Docker's Website](https://docs.docker.com/get-started/overview/){:target="_blank"}: Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.


## Quick Start

The first step is to install docker. You can do this on any ubuntu linux

```bash
sudo apt-get update
sudo apt  install docker.io
```

```bash
sudo docker info

```
ubuntu@ip-10-0-15-223:~$ sudo docker info
Client:
 Context:    default
 Debug Mode: false

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 20.10.21
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 io.containerd.runtime.v1.linux runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 
 runc version: 
 init version: 
 Security Options:
  apparmor
  seccomp
   Profile: default
  cgroupns
 Kernel Version: 5.19.0-1025-aws
 Operating System: Ubuntu 22.04.2 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 1
 Total Memory: 965.7MiB
 Name: ip-10-0-15-223
 ID: LOLA:J7IH:363C:AN4D:LAA6:F2RP:R7VA:7BTV:F3FG:YFSH:XB4M:B2FV
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false

ubuntu@ip-10-0-15-223:~$
```

sudo docker images

docker images

sudo usermod -aG docker ubuntu
newgrp docker

docker run alpine bash/pwd
docker run alpine bash/ls
docker run alpine bash/whoami


## Working with Images

docker images
ubuntu@ubuntu:~$ docker rmi alpine

docker ps

docker ps -a

docker rm 39c0bbdce667

docker pull ubuntu

docker images

docker run --name container1 -it ubuntu bash

`exit`

docker start container1

docker ps -a


## Building a docker image

## Adding Non-privilaged User

## DockerHub



