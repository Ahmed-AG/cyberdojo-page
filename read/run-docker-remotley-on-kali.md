---
layout: reads
title:  "Run Docker remotley on kali Linux server"
date:   06-10-2023
author: "Ahmed Abugharbia"
author_link: "https://twitter.com/aagsec"
---

There are many reasons why we might need to run docker remotly. Since docker runs  

### On the server side

- Run `sudo systemctl status docker` to check the status and verity service configuration file `options.conf`

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

Notice the line: `Loaded: loaded (/lib/systemd/system/docker.service; enabled; preset: enabled)`

- Add `-H tcp://0.0.0.0:2375` to ExecStart under /etc/systemd/system/docker.service.d/options.conf

```bash
ExecStart=/usr/sbin/dockerd -H tcp://0.0.0.0:2375 -H fd:// --containerd=/run/containerd/containerd.sock $DOCKER_OPTS
```
- Retstart docker service

```bash
sudo systemctl restart docker
```

### On the client side

- Set DOCKER_HOST to the IP address of your server

```bash
export DOCKER_HOST=tcp://<IP_ADDRESS>:2375
```
- Try to run docker commands 

```bash
% docker info
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc., v0.8.2)
  compose: Docker Compose (Docker Inc., v2.6.1)
  extension: Manages Docker extensions (Docker Inc., v0.2.7)
  sbom: View the packaged-based Software Bill Of Materials (SBOM) for an image (Anchore Inc., 0.6.0)
  scan: Docker Scan (Docker Inc., v0.17.0)

Server:
 Containers: 2
  Running: 0
  Paused: 0
  Stopped: 2
 Images: 7
 Server Version: 20.10.23+dfsg1
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
 Runtimes: io.containerd.runtime.v1.linux runc io.containerd.runc.v2
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1.6.18~ds1-1+b2
 runc version: 1.1.4+ds1-1+b3
 init version: 
 Security Options:
  apparmor
  seccomp
   Profile: default
  cgroupns
 Kernel Version: 6.0.0-kali3-amd64
 Operating System: Kali GNU/Linux Rolling
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 1.927GiB
 Name: kali
 ID: MLGX:2FEC:NTHP:SIHE:PZAK:KCR6:I6C4:ES53:DPLN:AHYP:LG6D:R4CS
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false

WARNING: API is accessible on http://0.0.0.0:2375 without encryption.
         Access to the remote API is equivalent to root access on the host. Refer
         to the 'Docker daemon attack surface' section in the documentation for
         more information: https://docs.docker.com/go/attack-surface/
% 
```

### Encrypting traffic
TODO