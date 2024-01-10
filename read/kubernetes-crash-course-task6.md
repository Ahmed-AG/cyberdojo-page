---
layout: reads
title:  "Kubernetes Crash Course - Task 5"
date:   1-9-2024
author: "Ahmed Abugharbia"
author_link: "https://www.linkedin.com/in/ahmadabugharbieh/"
---

### Task 6: Network Policies

So far we have created two different projects, we have created a project in a `blue` namespace and another in the `green` namespace. What if we needed to control network traffic between services or pods?
Let us do the following

make sure you have two deployments `blue` and `green`
```bash
DEPLOYMENT=blue
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass --namespace $DEPLOYMENT
kubectl apply -f example1-mongoApp/backend-mongo-db.yaml --namespace $DEPLOYMENT
kubectl apply -f example1-mongoApp/mongodb-configmap.yaml --namespace $DEPLOYMENT
kubectl apply -f example1-mongoApp/frontend-mongo-express.yaml --namespace $DEPLOYMENT
sleep 60
minikube service frontend-mongo-express -n $DEPLOYMENT


DEPLOYMENT=green
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass --namespace $DEPLOYMENT
kubectl apply -f example1-mongoApp/backend-mongo-db.yaml --namespace $DEPLOYMENT
kubectl apply -f example1-mongoApp/mongodb-configmap.yaml --namespace $DEPLOYMENT
kubectl apply -f example1-mongoApp/frontend-mongo-express-green.yaml --namespace $DEPLOYMENT
sleep 60
minikube service frontend-mongo-express -n $DEPLOYMENT
```

The above will take a couple of minutes. To verify your work you can use your browser or run:

```bash
kubectl get pods -o wide -n blue
kubectl get pods -o wide -n green
```
```
$ kubectl get pods -o wide -n blue
kubectl get pods -o wide -n green
NAME                                                READY   STATUS    RESTARTS        AGE   IP              NODE       NOMINATED NODE   READINESS GATES
backend-mongodb-deployment-97bb5c688-pl6vm          1/1     Running   2 (148m ago)    8h    10.244.120.80   minikube   <none>           <none>
frontend-mongo-express-deployment-db9c8bd6b-rgw64   1/1     Running   53 (140m ago)   8h    10.244.120.79   minikube   <none>           <none>
NAME                                                READY   STATUS    RESTARTS       AGE   IP              NODE       NOMINATED NODE   READINESS GATES
backend-mongodb-deployment-97bb5c688-mzx96          1/1     Running   2 (148m ago)   8h    10.244.120.82   minikube   <none>           <none>
frontend-mongo-express-deployment-db9c8bd6b-hkfnv   1/1     Running   2 (148m ago)   8h    10.244.120.81   minikube   <none>           <none>
```

This should show you the IP addresses of all of your pods. Once our environment is built, let us access the front end on the `blue` deployment then try to end the other pods
```bash
kubectl exec -ti <POD NAME> -n blue -- /bin/bash
ifconfig
ping <Blue Frontend IP>
ping <Green Frontend IP>
ping <Green Backend IP>
```

```
$ kubectl exec -ti frontend-mongo-express-deployment-db9c8bd6b-rgw64 -n blue -- /bin/bash
frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app# ifconfig
eth0      Link encap:Ethernet  HWaddr 7E:CA:CE:ED:C2:76  
          inet addr:10.244.120.79  Bcast:0.0.0.0  Mask:255.255.255.255
          UP BROADCAST RUNNING MULTICAST  MTU:1480  Metric:1
          RX packets:2431 errors:0 dropped:0 overruns:0 frame:0
          TX packets:3325 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:736401 (719.1 KiB)  TX bytes:275878 (269.4 KiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app# ping 10.244.120.80 -c 3
PING 10.244.120.80 (10.244.120.80): 56 data bytes
64 bytes from 10.244.120.80: seq=0 ttl=63 time=0.124 ms
64 bytes from 10.244.120.80: seq=1 ttl=63 time=0.113 ms
64 bytes from 10.244.120.80: seq=2 ttl=63 time=0.140 ms

--- 10.244.120.80 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.113/0.125/0.140 ms
frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app# ping 10.244.120.82 -c 3
PING 10.244.120.82 (10.244.120.82): 56 data bytes
64 bytes from 10.244.120.82: seq=0 ttl=63 time=0.252 ms
64 bytes from 10.244.120.82: seq=1 ttl=63 time=0.121 ms
64 bytes from 10.244.120.82: seq=2 ttl=63 time=0.086 ms

--- 10.244.120.82 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.086/0.153/0.252 ms
frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app# ping 10.244.120.81 -c 3
PING 10.244.120.81 (10.244.120.81): 56 data bytes
64 bytes from 10.244.120.81: seq=0 ttl=63 time=0.623 ms
64 bytes from 10.244.120.81: seq=1 ttl=63 time=0.180 ms
64 bytes from 10.244.120.81: seq=2 ttl=63 time=0.115 ms

--- 10.244.120.81 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.115/0.306/0.623 ms
frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app#
```

Notice that access is wide open!

### Apply Network Policies
There are multiple ways to apply network access in K8s. We will give one example that uses `apiVersion: networking.k8s.io/v1`. As a prerequisite, `Minikube` needs to be restarted with the `--cni calico`. To do so run the following:
```bash
minikube stop
minikube start --cni calico
```

This will enable network policies. Once Minikube is restarted we will apply [./example1-mongoApp/network-policy.yaml](https://github.com/Ahmed-AG/k8s-quick-start-tutorial/blob/main/example1-mongoApp/network-policy.yaml). Let us examine the major sections:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: network-policy
spec:
  podSelector:
    matchLabels:
      app: backend-mongodb
```

The above section dictates that we will create a `network-policy` resource that will be applied on pods that have the label: `backend-mongodb`. We can apply this network-policy on any Namespoace we want. Next, we need to set the rules. We want to only allow traffic from pods that have the label `app: frontend-mongo-express` and lives in the `green` namespace:
```
  policyTypes:
    - Ingress
  ingress:
    - from:
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: green
        - podSelector:
            matchLabels:
              app: frontend-mongo-express
```
Note that the actual file have many other commented out sections. feel free to explore those.
Let us apply this `network-policy` on the `green` namespace for this example:

```bash
kubectl apply -f example1-mongoApp/network-policy.yaml -n green
```

Try to access the Frontend pod on the blue namespace and try to ping the Backend on the blue, the Backend on the green, and the Frontend on the green:

```bash
$ kubectl exec -ti frontend-mongo-express-deployment-db9c8bd6b-rgw64 -n blue -- /bin/bash
frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app# ping 10.244.120.80
PING 10.244.120.80 (10.244.120.80): 56 data bytes
64 bytes from 10.244.120.80: seq=0 ttl=63 time=0.327 ms
64 bytes from 10.244.120.80: seq=1 ttl=63 time=0.096 ms
^C
--- 10.244.120.80 ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.096/0.211/0.327 ms
frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app# ping 10.244.120.82
PING 10.244.120.82 (10.244.120.82): 56 data bytes
^C
--- 10.244.120.82 ping statistics ---
4 packets transmitted, 0 packets received, 100% packet loss
frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app# ping 10.244.120.81
PING 10.244.120.81 (10.244.120.81): 56 data bytes
64 bytes from 10.244.120.81: seq=0 ttl=63 time=0.511 ms
64 bytes from 10.244.120.81: seq=1 ttl=63 time=0.102 ms
64 bytes from 10.244.120.81: seq=2 ttl=63 time=0.084 ms
^C
--- 10.244.120.81 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.084/0.232/0.511 ms
frontend-mongo-express-deployment-db9c8bd6b-rgw64:/app# exit
$
```

Great! Backend seems to be protected now. Let us see if the Frontend on the green namespace can access the Backend on the green namespace (Same Namespace):
```bash
kubectl exec -ti frontend-mongo-express-deployment-db9c8bd6b-hkfnv -n green -- /bin/bash
frontend-mongo-express-deployment-db9c8bd6b-hkfnv:/app# ping 10.244.120.82 -c 3
PING 10.244.120.82 (10.244.120.82): 56 data bytes
64 bytes from 10.244.120.82: seq=0 ttl=63 time=0.160 ms
64 bytes from 10.244.120.82: seq=1 ttl=63 time=0.067 ms
64 bytes from 10.244.120.82: seq=2 ttl=63 time=0.102 ms

--- 10.244.120.82 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.067/0.109/0.160 ms
frontend-mongo-express-deployment-db9c8bd6b-hkfnv:/app# exit
```

Sounds great! It seems that you have successfully protected the Backend on the green namespace deployment! Congratulation!

### References:
- [https://kubernetes.io/docs/concepts/services-networking/network-policies/](https://kubernetes.io/docs/concepts/services-networking/network-policies/) 
- A great resource for learning Kubernetes is this 4-hour [Youtube video](https://www.youtube.com/watch?v=X48VuDVv0do&t=3167s) by [TechWorld with Nana](https://www.youtube.com/@TechWorldwithNana)
