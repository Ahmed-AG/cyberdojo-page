---
layout: reads
title:  "Kubernetes Crash Course - Part 1"
date:   1-1-2024
author: "Ahmed Abugharbia"
author_link: "https://www.linkedin.com/in/ahmadabugharbieh/"
---
### Introduction
Kubernetes, often abbreviated as K8s, is an open-source container orchestration platform. It automates the deployment, scaling, and management of containerized applications. Originally developed by Google, Kubernetes has gained widespread adoption in managing containerized workloads and services.

#### Basic Kubernetes Components:

- Pods: The smallest deployable unit in Kubernetes, consisting of one or more containers that share storage and networking. They're scheduled together on the same node. It is an abstraction over the container run time, Docker for

- **Nodes:** These are the individual machines (physical or virtual) in a Kubernetes cluster where containers are deployed. Each node has services to run applications in the form of pods.

- Clusters: A set of nodes that work together. Clusters are the foundation of Kubernetes; they consist of at least one master node and multiple worker nodes.

- Master Node: Controls the Kubernetes cluster and manages its workload. It coordinates all activities in the cluster such as scheduling, scaling, and updating applications.

- Kubelet: An agent running on each node that communicates with the master node and manages the pods and containers on the node.

- Kube-proxy: Maintains network rules on nodes. It enables communication between different pods and services within the cluster.

- Controller Manager: Manages controller processes that regulate the state of the cluster, such as deployments, replica sets, and stateful sets.

- Scheduler: Assigns pods to nodes based on resource requirements and other constraints.

- Etcd: A distributed key-value store that stores the cluster's configuration data, representing the state of the cluster at any given time.

These components work together to ensure that applications run efficiently, are scalable, and can easily be managed in a containerized environment.

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

---

### Task 1: Basic `kubectl` commands
Let us explore our Minikube environment:
Run the help to learn about the basic commands:

```bash
kubectl -h
```
```
$ kubectl -h
kubectl controls the Kubernetes cluster manager.

 Find more information at: https://kubernetes.io/docs/reference/kubectl/

Basic Commands (Beginner):
  create          Create a resource from a file or from stdin
  expose          Take a replication controller, service, deployment or pod and expose it as a new Kubernetes service
  run             Run a particular image on the cluster
  set             Set specific features on objects

Basic Commands (Intermediate):
  explain         Get documentation for a resource
  get             Display one or many resources
  edit            Edit a resource on the server
  delete          Delete resources by file names, stdin, resources and names, or by resources and label selector
...
```
Notice that we can create, delete, get and describe resources. We will later work with the following resources:
- Pods: An abstraction over a container run time such as Docker.
- Deployments: we don't directly work with pods. Instead, we create deployments that could have one or multiple pods performing the same task.
- Services: Provide way to access a set of deployments (and therefore pods), typically through an endpoint (IP Addresses and Names).
- ConfigMaps: We will use ConfigmMps to store information that is needed accross deployments.
- Secrets: Very similar to ConfigMaps except it is meant for secret values. We will use Secrets to store Database credentials.


#### Create a deployment
The following command will instruct K8s to create a deployment and a pod with nginx docker container image `nginx`. It will set a lot of defaults as well

```bash
kubectl create deployment nginx --image=nginx
```
Let us explore the deployment we created. Run the following command:

```bash
kubectl get deployment
```

```bash
$kubectl get deployment
NAME                                READY   UP-TO-DATE   AVAILABLE   AGE
nginx                               1/1     1            1           14s
```

We can also explore more:
```bash
kubectl get pods
```
```bash
$ kubectl get pods
NAME                                                READY   STATUS    RESTARTS   AGE
nginx-7854ff8877-6wq4n                              1/1     Running   0          3m23s
```

We can use the `-o wide` option to show more information such as the IP addresses:

```bash
kubectl get pods -o wide
```

```
$ kubectl get pods -o wide
NAME                                                READY   STATUS    RESTARTS   AGE     IP            NODE       NOMINATED NODE   READINESS GATES
nginx-7854ff8877-6wq4n                              1/1     Running   0          5m11s   10.244.0.31   minikube   <none>           <none>
```

We can also `describe` resources using the command `kubectl describe pods <POD-NAME>`:

```bash
kubectl describe pods nginx-7854ff8877-6wq4n
```
```
$ kubectl describe pods nginx-7854ff8877-6wq4n
Name:             nginx-7854ff8877-6wq4n
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.59.100
Start Time:       Fri, 22 Dec 2023 19:34:20 -0600
Labels:           app=nginx
                  pod-template-hash=7854ff8877
Annotations:      <none>
Status:           Running
IP:               10.244.0.31
IPs:
  IP:           10.244.0.31
Controlled By:  ReplicaSet/nginx-7854ff8877
Containers:
  nginx:
    Container ID:   docker://455c96e8e59fb29fd3aabe439de64c9e0b1b1de0dc691fd0389afbdab382a025
    Image:          nginx
...
```

##### Exploring the pods
So far we have created one `deployment` and one `pod`. Use the following to execute commands inside a specific pod (Container): `kubectl exec  <pod-name> -- <Shell Command>` 

```bash
kubectl exec nginx-7854ff8877-6wq4n -- uname -a
```
```
$ kubectl exec nginx-7854ff8877-6wq4n -- uname -a
Linux nginx-7854ff8877-6wq4n 5.10.57 ###1 SMP Tue Nov 7 06:51:54 UTC 2023 x86_64 GNU/Linux
```

We can also get a shell on a container:
```bash
kubectl exec -ti nginx-7854ff8877-6wq4n -- /bin/bash
```
```
$ kubectl exec -ti nginx-7854ff8877-6wq4n -- /bin/bash
root@nginx-7854ff8877-6wq4n:/# uname -a
Linux nginx-7854ff8877-6wq4n 5.10.57 ###1 SMP Tue Nov 7 06:51:54 UTC 2023 x86_64 GNU/Linux
root@nginx-7854ff8877-6wq4n:/#
```

Finally, we can read logs from a pod using `kubectl logs <pod-name>`
```bash
kubectl logs nginx-7854ff8877-6wq4n
```
```
$ kubectl logs nginx-7854ff8877-6wq4n
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2023/12/23 01:34:33 [notice] 1###1: using the "epoll" event method
2023/12/23 01:34:33 [notice] 1###1: nginx/1.25.3
2023/12/23 01:34:33 [notice] 1###1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2023/12/23 01:34:33 [notice] 1###1: OS: Linux 5.10.57
2023/12/23 01:34:33 [notice] 1###1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2023/12/23 01:34:33 [notice] 1###1: start worker processes
2023/12/23 01:34:33 [notice] 1###1: start worker process 28
2023/12/23 01:34:33 [notice] 1###1: start worker process 29
```

---

### Task 2: Building a sample application

Kubernetes support building infrastructure using configuration files. K8s configuration files are YAML or JSON files used to define and manage Kubernetes resources, such as pods, deployments, services, etc. These files contain specifications that describe the desired state of the resources you want to create or modify within a Kubernetes cluster.

Here are some key components and sections commonly found in Kubernetes configuration files:
- API Version: Specifies the version of the Kubernetes API that the object uses.
-Kind: Defines the type of Kubernetes resource being created, such as Pod, Deployment, Service, etc.
- Metadata: Contains information like the name, labels, and annotations for the resource.
- Spec: Describes the desired state of the resource. This section varies based on the resource type. For example:
  - Pods: Contains specifications for containers, volumes, and other settings.
  - Deployments: Includes information about replicas, pod templates, update strategies, etc.
  - Services: Defines how the service should be exposed, its ports, selectors, etc.
- Selectors: Often used in conjunction with services or controllers to define how resources are associated or targeted.
- Annotations: Additional information or metadata that can be added to the resource for various purposes like documentation, tooling, etc.

We have three configuration files being used for this tutorial. You can find them [here](https://github.com/Ahmed-AG/k8s-quick-start-tutorial/blob/main/example1-mongoApp/)

### Build a sample application
In this example, we will build a sample application that consists of the following:
1. A MongoDB as the `Backend`. Accessible only for the Frontend and consists of one Pod
2. A Mongo-express as the `Frontend`. Accessible from the outside and consists of one Pod

To do that, we will use three different configuration files as follows:
- [backend-mongo-db.yaml](https://github.com/Ahmed-AG/k8s-quick-start-tutorial/blob/main/example1-mongoApp/backend-mongo-db.yaml): Will create a Deployment and a Service for the backend
- [frontend-mongo-express.yaml](https://github.com/Ahmed-AG/k8s-quick-start-tutorial/blob/main/example1-mongoApp/frontend-mongo-express.yaml): Will create a Deployment and a Service for the frontend
- [mongodb-configmap.yaml](https://github.com/Ahmed-AG/k8s-quick-start-tutorial/blob/main/example1-mongoApp/mongodb-configmap.yaml): Will create ConfigMap that will have the backend's name
- Finally, we will create `sectret` that has the Database user name and password. We will do that though the command line

We will begin with creating the secret.

### Creating the secret:
`Secrets` are a way to securely store sensitive information, such as passwords, tokens, or keys. They're designed to help manage sensitive data access within Kubernetes deployments. Secrets provide a layer of abstraction and security by encoding and storing sensitive information separately from pod definitions or application code.

Kubernetes secrets can be used by referencing them in pods or containers, allowing applications to access sensitive information without exposing it directly within the code or configuration files. Secrets are stored within the cluster `etcd` and can be accessed by authorized entities.

Both the backend and the frontend will need to access the secret we will create. On the backend we will need to set the username and password of the Database. And on the front end we will need to configure the right username and password to be used.

So, we will create two secrets:
- mongo-username
- mongo-password
Because we want to be able to do this in a pipeline, we chose to use the `kubectl` to create the secrets. Run the following (you can choose your password):

```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
```
To verify that the above was successful:
```bash
kubectl get secrets
```
```
$ kubectl get secrets
NAME             TYPE     DATA   AGE
mongodb-secret   Opaque   2      5d
```
You can also run:
```bash
kubectl describe secrets mongodb-secret
```
```
$ kubectl describe secrets mongodb-secret
Name:         mongodb-secret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
mongo-password:  9 bytes
mongo-username:  9 bytes
```

---

### Task 3: Create the Backend

The full configuration file is [here](https://github.com/Ahmed-AG/k8s-quick-start-tutorial/blob/main/example1-mongoApp/backend-mongo-db.yaml). But let us dissect it.
This file will create two resources:
- A `Deployment` for the backend
- A `Service` for that backend

#### Backend Deployment

First we need to configure the resource Type and some Metadata
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-mongodb-deployment
  labels:
    app: backend-mongodb
```

Above sets a name for this deployment and also a label that will be used to reference this deployment later on.
Next,  we need to set some specifications:
```
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backend-mongodb
  template:
    metadata:
      labels:
        app: backend-mongodb
```
In the above code we set the replicas to `1` because we need one Pod. and we also set the selector to select the label `app: backend-mongodb`

Next, we need to set the container specification. We have an `Container Image` that is already configured with MongoDB. We will se that, and we will also set the default port.
```
    spec:
      containers:
      - name: backend-mongodb
        image: mongo
        ports:
        - containerPort: 27017
```
The Next step is for us to configure the username and password for the Database. We can do that by setting the environment variables `MONGO_INITDB_ROOT_USERNAME` and `MONGO_INITDB_ROOT_PASSWORD` inside the container. The values of those are being referenced from the `mongodb-secret` secret we set earlier.

```
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-username
        - name: MONGO_INITDB_ROOT_PASSWORD
          valueFrom: 
            secretKeyRef:
              name: mongodb-secret
              key: mongo-passwor
```
#### Creating the service
Finally, we are going to create service and tie it to the deployment we just created:
```
apiVersion: v1
kind: Service
metadata:
  name: backend-mongodb
spec:
  selector:
    app: backend-mongodb
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
```

Notice that we used the `app: backend-mongodb` as a selector and we exposed the same port `27017`. Notice also that we don't have anything that dictates wether we should expose access to this service externally. The default is that we will not.

#### Apply the Backend

```bash
kubectl apply -f example1-mogoApp/backend-mongo-db.yaml
```

---

### Task 4: Create the Frontend
#### ConfigMap
A ConfigMap in Kubernetes is an object used to store configuration data in key-value pairs. It provides a way to decouple configuration artifacts from container images, allowing you to manage configurations separately from the application code.

ConfigMaps are commonly used to store non-sensitive, configuration-specific data, such as environment variables, command-line arguments, configuration files, or other settings required by applications running in Kubernetes pods.

We need to configure the mongodb-configmap to store the `database_url: backend-mongodb` value for reference in the Frontend. [Full file is here](./example1-mongoApp/mongodb-configmap.yaml):

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: mongodb-configmap
data:
  database_url: backend-mongodb
```

#### Apply the ConfigMap
```bash
kubectl apply -f example1-mogoApp/mongodb-configmap.yaml
```

#### Frontend Deployment:
First, we need to set up the `Kind` as `Deployment`, the name and the same basic Replicas and Selector as before

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-mongo-express-deployment
  labels:
    app: frontend-mongo-express
spec:
  replicas: 1
  selector:
    matchLabels:
      app: frontend-mongo-express
  template:
    metadata:
      labels:
        app: frontend-mongo-express
```
Then, we will set a container image that is preconfigured with MongoExpress: `mongo-express`. We will also set the default port. And we will configure `ME_CONFIG_MONGODB_ADMINUSERNAME` and `ME_CONFIG_MONGODB_ADMINPASSWORD` environment variables
```
    spec:
      containers:
      - name: mongo-express
        image: mongo-express
        ports:
        - containerPort: 8081
        env:
        - name: ME_CONFIG_MONGODB_ADMINUSERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-username
        - name: ME_CONFIG_MONGODB_ADMINPASSWORD
          valueFrom: 
            secretKeyRef:
              name: mongodb-secret
              key: mongo-password
```
The last thing we need to add in the deployment is setting up the Database server name. We will do that using the ConfigMap data we set earlier
```
        - name: ME_CONFIG_MONGODB_SERVER
          valueFrom: 
            configMapKeyRef:
              name: mongodb-configmap
              key: database_url
```

#### Frontend Service:
The service for the frontend deployment is slightly different than the service do the backend deployment. In the frontend Service we will need to expose it to the internet:
```
apiVersion: v1
kind: Service
metadata:
  name: frontend-mongo-express
spec:
  selector:
    app: frontend-mongo-express
  type: LoadBalancer  
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
      nodePort: 30000
```
Notice that we set the `type` to `LoadBalancer`, which will expose this service externally. And we had to add `nodePort: 30000` which will set the port to be used externally.

#### Apply the Frontend
```bash
kubectl apply -f example1-mogoApp/frontend-mongo-express.yaml
```
Give it few minutes for all services to be created then move to the next step.

### Expose the Frontend using Minikube
```bash
minikube service frontend-mongo-express
```
The above command will expose `frontend-mongo-express` service and give it a public IP address
![Minikube exposing frontend-mongo-express](images/screenshot-minikube-expose.png?raw=true)

You can access the frontend by pointing your browser to the IP address that was assigned. Notice that Mongo-express allows you to interact with the backend which is the MongoDB server (Service)
![Firefox-mongoexpress](images/screenshot-firefox-mongoexpress.png)
User `admin` and `pass` to login to Mongo-Express.
Congratulations! Your Application is built!

<!-- ### Ingress

```bash
minikube addons enable ingress
```


```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
kubectl apply -f example2-mongoApp/backend-mongo-db.yaml
kubectl apply -f example2-mongoApp/mongodb-configmap.yaml
kubectl apply -f example2-mongoApp/frontend-mongo-express.yaml
kubectl apply -f example2-mongoApp/ingress.yaml
```

```bash
IP=$(kubectl get ingress -o json |jq -r .items[].status.loadBalancer.ingress[].ip)
echo $IP
sudo echo  >> /etc/hosts
sudo -- sh -c "echo '$IP my-frontend.com' >> /etc/hosts"
``` -->

### References:
- A great resource for learning Kubernetes is this 4-hour [Youtube video](https://www.youtube.com/watch?v=X48VuDVv0do&t=3167s) by [TechWorld with Nana](https://www.youtube.com/@TechWorldwithNana)