# cka

## What are the main components of the control plane?

<!-- notecardId: 1764010735532 -->

etcd
scheduler
controllers
api server

## What does etcd do?

<!-- notecardId: 1764010735537 -->

stores cluster-wide configuration and state data

## What does the scheduler do?

<!-- notecardId: 1764010735541 -->

determines the best node for new container deployments

## What is the purpose of controllers?

<!-- notecardId: 1764010735546 -->

manage node lifecycle, container replication, and system stability

## What does the api server do?

<!-- notecardId: 1764010735549 -->

acts as the central hub for cluster communication and management

## What is etcd?

<!-- notecardId: 1764010735553 -->

a distributed reliable key-value store that is simple and fast

## What is the difference between key-value store and relational data bases?

<!-- notecardId: 1764010735557 -->

key-value store 
does not require a schema
has no support for complex queries
has verry good performance
is very flexible
is best used for simple fast lookup

## How do you check the etcd version?

<!-- notecardId: 1764010735560 -->

```console
etcdctl version
```

## What is the default port for etcd?

<!-- notecardId: 1764010735564 -->

2379

## What command shows all the system pods?

<!-- notecardId: 1764010735568 -->

```console
kubectl get pods -n kube-system
```

## What command shows all keys stored in etcd?

<!-- notecardId: 1764010735572 -->

```console
kubectl exec etcd-master -n kube-system -- etcdctl get / --prefix --keys-only=true
```

## In a ha env how do the multiple etcd instances know about each other?

<!-- notecardId: 1764010735576 -->

through the initial-cluster-controller setting

## Where can you see the settings of each pod from the kube-system namespace?

<!-- notecardId: 1764010735580 -->

```console
/etc/kubernetes/manifest/
```

## Where can you find the services of the main control plane components?

<!-- notecardId: 1764010735585 -->

```console
/etc/systemd/system/kube-controller-manager.service
```

## What are the main components of the worker nodes?

<!-- notecardId: 1764010735588 -->

kubelet
kube proxy
pod

## What is the role of the kubelet?

<!-- notecardId: 1764010735592 -->

oversees node activities by managing container operations such as starting and stopping containers based on instructions from the master scheduler

## What is the kube proxy?

<!-- notecardId: 1764010735596 -->

runs in a pod on every node in the Kubernetes cluster
monitors for Service creations and configure network rules that redirect traffic to the corresponding pods

## How can you list objects with kubectl (ex: pods)?

<!-- notecardId: 1764010735599 -->

```console
kubectl get pods
```

## How can you see more details about objects with kubectl (ex: pod myapp)?

<!-- notecardId: 1764010735603 -->

```console
kubectl describe pod myapp
```

## What are the required configuration fields for a yml file?

<!-- notecardId: 1764010735607 -->

apiVersion:
kind: 
metadata:
spec:

## How does a pod yml config look like?

<!-- notecardId: 1764010735611 -->

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx
```

## How do you remove an object with kubectl (ex: pod myapp)?

<!-- notecardId: 1764010735615 -->

```console
kubectl delete pod myapp
```

## What does a replica set do?

<!-- notecardId: 1764010735619 -->

ensures high availability by creating and maintaining the desired number of pod replicas
it spans across multiple nodes on the cluster

## What is the difference between replicaSet and replication controller?

<!-- notecardId: 1764010735622 -->

replica set is the new way of managing pod replication
replication controller is the old way

## How does a replication controller yml look like?

<!-- notecardId: 1764010735626 -->

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: front-end
spec:
  replicas: 3
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx
```

## How do you execute a yml file(ex: pod.yml) with kubectl?

<!-- notecardId: 1764010735630 -->

```console 
kubectl create -f pod.yml
```

## How does a replica set yml file look like?

<!-- notecardId: 1764010735634 -->

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-replicaset
  labels:
    app: myapp
    type: front-end
spec:
  replicas: 3
  selector:
    matchLabels:
      type: front-end
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx
```

## Why do you have a selector section in the replica set yml?

<!-- notecardId: 1764010735638 -->

because replica set can apply to pods not created as part of the replica set creation

## What are two commands you can use to increase the number of pods in a replicat set without modifying the yml definition file?

<!-- notecardId: 1764010735642 -->

```console
kubectl scale --replicas=6 -f repset.yml
kubectl scale --replicas=6 replicaset myapp-repset
```

## What command can you use to update an existing object via yml definition file(ex: pod.yml)?

<!-- notecardId: 1764010735646 -->

```console
kubectl replace -f pod.yml
```

## What does a deployment do?

<!-- notecardId: 1764010735649 -->

automatically manages ReplicaSets and pods while providing enhanced features like rolling updates and rollbacks

## How does a deployment yml file look like?

<!-- notecardId: 1764010735653 -->

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
  labels:
    app: myapp
    type: front-end
spec:
  replicas: 3
  selector:
    matchLabels:
      type: front-end
  template:
    metadata:
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
```

## What command shows a summary of the entire cluster?

<!-- notecardId: 1764010735657 -->

```console
kubectl get all
```

## Create an nginx pod.

<!-- notecardId: 1764010735660 -->

```console
kubectl run nginx --image=nginx
```

## Generate a pod yaml file without creating it.

<!-- notecardId: 1764010735665 -->

```console
kubectl run nginx --image=nginx --dry-run=client -o yaml > nginx_pod.yaml
```

## Generate a deployment yaml file without creating it.

<!-- notecardId: 1764010735668 -->

```console
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx_deployment.yaml
```

## What does a service do?

<!-- notecardId: 1764010735672 -->

allows different sets of Pods to interact with each other

## How does a nodeport service yml file look like?

<!-- notecardId: 1764010735676 -->

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  ports:
    - targetPort: 80
      port: 80
      N: 30008
```

## What does node port service do?

<!-- notecardId: 1764010735680 -->

maps a specific node port (e.g., 30008) to the target port on your Pod (e.g., 80)
provides external access while keeping internal port targeting intact

## What is the valid range for node port?

<!-- notecardId: 1764010735685 -->

30000-32767

## Which parameter is mandatory from the ports section of the yaml file for node port?

<!-- notecardId: 1764010735688 -->

port

## What are the default values of nodePort and target port when only port parameter is specified in the yaml config of a node port?

<!-- notecardId: 1764010735692 -->

targetPort will have same value as port
nodePort will be a free port in the range of 30000-32767

## Is a NodePort service restricted to running on a single node?

<!-- notecardId: 1764010735696 -->

NO, a NodePort service runs by default across all nodes in the cluster

## What alogrithm does NodePort service use for load balancing?

<!-- notecardId: 1764010735699 -->

random

## What does a ClusterIP service do?

<!-- notecardId: 1764010735703 -->

it groups related pods under the same serivce and ip

## How does a ClusterIP service yml file look like?

<!-- notecardId: 1764010735707 -->

```yaml
apiVersion: v1
kind: Service
metadata:
  name: back-end
spec:
  type: ClusterIP
  ports:
    - port: 80
      targetPort: 80
  selector:
    app: myapp
    type: back-end
```

## What does a LoadBalancer service do?

<!-- notecardId: 1764010735710 -->

provides a single url to access your app

## How does a LoadBalancer service yml file look like in a supported cloud provider?

<!-- notecardId: 1764010735714 -->

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-lb
spec:
  type: LoadBalancer
  ports:
    - targetPort: 80
      port: 80
      nodePort: 30008
```

## What does a namespace do?

<!-- notecardId: 1764010735718 -->

it helps organize and isolate resources in your cluster

## What are the three namespaces created at startup?

<!-- notecardId: 1764010735721 -->

kube-system
default
kube-public

## How can a pod in one namespace reach another pod in a different namespace?

<!-- notecardId: 1764010735725 -->

by adding the other namespace to the other pod dns 
same namespace ex: mysql.connect("db-service")
diff namespace ex(namespace dev): mysql.connect("db-service.dev.svc.cluster.local")

## What is used to limit consumption of hardware resources in namespaces?

<!-- notecardId: 1764010735729 -->

ResourceQuota

## How does a ResourceQuota yaml file look like?

<!-- notecardId: 1764010735732 -->

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "4"
    requests.memory: 5Gi
    limits.cpu: "10"
    limits.memory: 10Gi
```

## Given the following dns service name db-service.dev.svc.cluster.local, explain the name components.

<!-- notecardId: 1764010735736 -->

service name : db-service
namespace : dev
subdomain for service : svc
domain : cluster.local

## List all pods in the kube-system namespace.

<!-- notecardId: 1764010735740 -->

```console
kubectl get pods --namespace=kube-system
```

## In what section of the yaml file can you specify the namespace?

<!-- notecardId: 1764010735744 -->

metadata

## How does a namespace yaml file look like?

<!-- notecardId: 1764010735747 -->

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

## How can you set the default namespace for other cli commands to dev?

<!-- notecardId: 1764010735751 -->

```console
kubectl config set-context $(kubectl config current-context) --namespace=dev
```

## List pods in all namespaces.

<!-- notecardId: 1764010735755 -->

```console
kubectl get pods --all-namespaces
```

