---
layout: reads
title:  "Run Docker remotley on kali Linux server"
date:   06-10-2023
author: "Ahmed Abugharbia"
author_link: "https://twitter.com/aagsec"
---

## Introduction
There are many reasons why we might need to run docker remotly. Since docker runs  

### On the server side

Run `sudo systemctl status docker` to check the status and verity service configuration file `options.conf`

```bash
┌──(kali㉿kali)-[~]
└─$ sudo systemctl status docker                                     
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; preset: enabled)
     Active: active (running) since Sat 2023-06-10 09:51:40 EDT; 2h 38min ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 94373 (dockerd)
      Tasks: 11
     Memory: 924.2M
        CPU: 2min 19.742s
     CGroup: /system.slice/docker.service
             └─94373 /usr/sbin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```

Notice the line:
`     Loaded: loaded (/lib/systemd/system/docker.service; enabled; preset: enabled)`

Add `-H tcp://0.0.0.0:2375` to `ExecStart` under `/etc/systemd/system/docker.service.d/options.conf` 

```bash
ExecStart=/usr/sbin/dockerd -H tcp://0.0.0.0:2375 -H fd:// --containerd=/run/containerd/containerd.sock $DOCKER_OPTS
```
### On the client side

On the client side, set DOCKER_HOST to the IP address of your server

```bash
export DOCKER_HOST=tcp://<IP_ADDRESS>:2375
```

Retstart docker service

```bash
sudo systemctl restart docker
```
