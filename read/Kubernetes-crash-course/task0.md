---
layout: reads
title:  "Kubernetes Crash Course - Task 0"
date:   1-1-2024
author: "Ahmed Abugharbia"
author_link: "https://www.linkedin.com/in/ahmadabugharbieh/"
---
### Task 0: Set up you testing environment

#### MiniKube
Minikube is a tool that allows you to run a single-node Kubernetes cluster locally on your computer. It's designed to enable developers to learn and experiment with Kubernetes or to develop applications locally before deploying them to a larger Kubernetes cluster.

##### Install Minikube

Follow the steps in the here to install and start Minikube: [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)


#### kubectl

`kubectl` is the command-line interface (CLI) used to interact with Kubernetes clusters. It allows users to execute commands against Kubernetes clusters to deploy applications, manage and inspect cluster resources, and perform various administrative tasks.

##### Install kubectl
kubectl will be configured automatically to authenticate to Minikube during the minikube installation process (check `~/.kube/config`). However, you might still need to install `kubectl` itself. To install `kubectl` Follow the steps here:[https://kubernetes.io/docs/tasks/tools/]( https://kubernetes.io/docs/tasks/tools/)

#### Clone examples repository

Once you have your environment ready, clone the following repository

```bash
git clone https://github.com/Ahmed-AG/k8s-quick-start-tutorial.git
```

### Next
[Task 1: Basic `kubectl` commands](/read/Kubernetes-crash-course/task1.html)
