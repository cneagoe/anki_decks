# k8s

## What does the etcd component do?

<!-- notecardId: 1763281862228 -->

functions as a key-value store, an internal database

## What does the scheduler do?

<!-- notecardId: 1763281862233 -->

it distributes work across the containers

## What does the api server do?

<!-- notecardId: 1763281862237 -->

serves as the frontend for k8s, allows interaction with the cluster

## What does the controler do?

<!-- notecardId: 1763281862240 -->

the notice when anything goes down and bring them back up

## What does the container run time do?

<!-- notecardId: 1763281862244 -->

it is used to run containers, can be docker, containerd or something else

## What does the kubelet do?

<!-- notecardId: 1763281862247 -->

it is the agent running on all worker nodes, ensures containers run properly

## On what node doest the kube-apiserver run?

<!-- notecardId: 1763281862250 -->

master

## What does the kubectl run command do?

<!-- notecardId: 1763281862252 -->

it deploys an application on the cluster

## What does the kubectl cluster-info command do?

<!-- notecardId: 1763281862254 -->

provides information about the cluster

## what does the kubectl get nodes command do?

<!-- notecardId: 1763281862257 -->

list all nodes in the cluster

## What is the main purpose of the ctr command line tool?

<!-- notecardId: 1763281862260 -->

debugging, should not be used for regular use cases, use nerdcli instead

## What is nerdcli?

<!-- notecardId: 1763281862262 -->

a cli tool for containerd that can run all the commands normaly run with the docker command line

## What is the main purpose of the crictl command line tool?

<!-- notecardId: 1763281862264 -->

debugging containers, it works with CRI compatible runtimes

## What is the CRI?

<!-- notecardId: 1763281862267 -->

k8s interface with container runtime

## How do you find what os are the nodes running?

<!-- notecardId: 1763281862269 -->

```bash
kubectl get nodes -o wide
```

## What is a pod?

<!-- notecardId: 1763281862271 -->

a single instance of an application

## Create a pod running an nginx server.

<!-- notecardId: 1763281862273 -->

```bash
kubectl run nginx --image=nginx
```

## Get detailed info about a pod runing nginx.

<!-- notecardId: 1763281862276 -->

```bash
kubectl describe pod nginx
```

## What does the replication controler do?

<!-- notecardId: 1763281862278 -->

ensures high availability by bringing up pods when they are down

## What does a replica set do?

<!-- notecardId: 1763281862280 -->

is a newer version of replication controller
ensures high availability by bringing up pods when they are down

## What are the 4 main components of any yml resource definition?

<!-- notecardId: 1763281862282 -->

apiVersion
kind
metadata
spec

## What are two of the most common used metadata items in yml?

<!-- notecardId: 1763281862284 -->

name
labels

## How do you create a resource using a yml file?

<!-- notecardId: 1763281862287 -->

```bash
kubectl create -f rc-definition.yml
```

## How do you see details about any replication rules?

<!-- notecardId: 1763281862289 -->

```bash
kubectl get replicationcontroller
```

## How do you see details about running pods?

<!-- notecardId: 1763281862291 -->

```bash
kubectl get pods
```

## What is required extra in yml for replica set?

<!-- notecardId: 1763281862293 -->

a selector section where you match labels of pods that should be managed by the replica set
```console
selector:
    matchLabels:
        type: front-end
```

## What can replica set be used that replication controller can't?

<!-- notecardId: 1763281862295 -->

monitoring already deployed pod

## Assuming you have deployed 3 pods how can you add extra 3 pods of the same kind using replicaset without modifying yml file?

<!-- notecardId: 1763281862298 -->

```bash
kubectl scale --replicas=6 -f replicaset-definition.yml
```
or
```bash
kubectl scale --replicas=6 replicaset myapp-replicaset
```

## How can you remove a replicaset and underlying pods?

<!-- notecardId: 1763281862300 -->

```bash
kubectl delete replicaset myapp-replicaset
```

## How can you update the yml of an existing replicaset?

<!-- notecardId: 1763281862302 -->

```bash
kubectl replace -f replicaset-definition.yml
```

## What does a deployment do?

<!-- notecardId: 1763281862304 -->

rolling updates
rollbacks
pause/resume pod deployment

## What is the hierarhical order between replicaset pods and deployments?

<!-- notecardId: 1763281862306 -->

deployment
creates
replicaset
creates
pod

## What is the main difference between replica set an deployment?

<!-- notecardId: 1763281862309 -->

a deployment can handle update automatically
if you only use replica sets you need to do it manually

## How do you see all objects created in a cluster?

<!-- notecardId: 1763281862311 -->

```bash
kubectl get all
```

## How do you see the status of a rollout?

<!-- notecardId: 1763281862313 -->

```bash
kubectl rollout status deployment/myapp-deployment
```

## What does the recreate deployment strategy do?

<!-- notecardId: 1763281862315 -->

destroy all pods and create new ones

## What does the rolling update deployment strategy do?

<!-- notecardId: 1763281862317 -->

replace pods with new version one by one

## What is the default deployment strategy?

<!-- notecardId: 1763281862320 -->

rolling update

## How do you rollback a deployment?

<!-- notecardId: 1763281862322 -->

```bash
kubectl rollout undo deployment myapp-deployment
```

## How can you update the deployment image from cli?

<!-- notecardId: 1763281862324 -->

```bash
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
```

## How can you see past rollouts?

<!-- notecardId: 1763281862326 -->

```bash
kubectl rollout history deployment/myapp-deployment
```

## What criteria has to be met in for k8s networking?

<!-- notecardId: 1763281862328 -->

all containers/pods can communicate with one another without NAT
all nodes can comunicate with containers and vice versa

## What is NAT?

<!-- notecardId: 1763281862330 -->

a process used by a router or firewall to remap a private IP address to a public one, allowing multiple devices on a local network to share a single public IP address to access the internet

## What does a node port service do?

<!-- notecardId: 1763281862332 -->
 
listens to a port on the node and forwards that trafic to a port on the pod

## What is the valid range of ports for a node port?

<!-- notecardId: 1763281862335 -->

30000 - 32767

## How do you list existing services?

<!-- notecardId: 1763281862337 -->

```bash
kubectl get service
```

## How do you create a service?

<!-- notecardId: 1763281862339 -->

```bash
kubectl create -f service-definition.yml
```

## What algorithm is used by node port for load balancing?

<!-- notecardId: 1763281862341 -->

random

## What is the cluster ip service used for?

<!-- notecardId: 1763281862344 -->

enabling communication between categories of pods such as frontend, backend, db

## What is load balancer service used for?

<!-- notecardId: 1763281862351 -->

spreading trafic load between pods

## What is the type of the default kubernetes service?

<!-- notecardId: 1763281862353 -->

cluster-ip


<!--aoe-->                                                                                                                                                                                                                             