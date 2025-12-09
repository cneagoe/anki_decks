# cka

## What are the main components of the control plane?

<!-- notecardId: 1764576530413 -->

etcd
scheduler
controllers
api server

## What does etcd do?

<!-- notecardId: 1764576530423 -->

stores cluster-wide configuration and state data in a key-value store

## What does the scheduler do?

<!-- notecardId: 1764576530425 -->

determines the best node for new pods deployments

## What is a controller?

<!-- notecardId: 1764576530427 -->

a control loop that watches the state of your cluster and makes or requests changes where needed

## What does the api server do?

<!-- notecardId: 1764576530430 -->

acts as the central hub for cluster communication and management

## What is the difference between key-value store and relational data bases?

<!-- notecardId: 1764576530432 -->

key-value store 
does not require a schema
has no support for complex queries
has verry good performance
is very flexible
is best used for simple fast lookup

## How do you check the etcd version?

<!-- notecardId: 1764576530434 -->

```console
etcdctl version
```

## What is the default port for etcd?

<!-- notecardId: 1764576530436 -->

2379

## What command shows all the system pods?

<!-- notecardId: 1764576530439 -->

```console
kubectl get pods -n kube-system
```

## What command shows all keys stored in etcd?

<!-- notecardId: 1764576530441 -->

```console
etcdctl get / --prefix --keys-only=true
```

## How do you execute a etcdl command in the etcd-master pod of the kube-system namespace?

<!-- notecardId: 1764577706668 -->

```console
kubectl exec etcd-master -n kube-system -- etcdl something
```

## In a ha env how do the multiple etcd instances know about each other?

<!-- notecardId: 1764576530443 -->

through the initial-cluster config setting

## Where can you see the settings of each pod from the kube-system namespace?

<!-- notecardId: 1764576530445 -->

```console
/etc/kubernetes/manifest/
```

## Where can you find the services of the main control plane components?

<!-- notecardId: 1764576530447 -->

```console
/etc/systemd/system/kube-controller-manager.service
```

## What are the main components of the worker nodes?

<!-- notecardId: 1764576530450 -->

kubelet
kube proxy
pod

## What is the role of the kubelet?

<!-- notecardId: 1764576530452 -->

takes the PodSpecs provided and ensures that the containers described in those PodSpecs are running and healthy

## What is the kube proxy?

<!-- notecardId: 1764576530454 -->

runs in a pod on every node in the Kubernetes cluster
monitors for Service creations and configure network rules that redirect traffic to the corresponding pods

## How can you list objects with kubectl (ex: pods)?

<!-- notecardId: 1764576530456 -->

```console
kubectl get pods
```

## How can you see more details about objects with kubectl (ex: pod myapp)?

<!-- notecardId: 1764576530462 -->

```console
kubectl describe pod myapp
```

## What are the required configuration fields for a yml file?

<!-- notecardId: 1764576530468 -->

apiVersion:
kind: 
metadata:
spec:

## How does a pod yml config look like?

<!-- notecardId: 1764576530474 -->

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

<!-- notecardId: 1764576530480 -->

```console
kubectl delete pod myapp
```

## What does a replica set do?

<!-- notecardId: 1764576530485 -->

ensures high availability by creating and maintaining the desired number of pod replicas
it spans across multiple nodes on the cluster

## What is the difference between replicaSet and replication controller?

<!-- notecardId: 1764576530488 -->

replica set is the new way of managing pod replication
replication controller is the old way

## How do you execute a yml file(ex: pod.yml) with kubectl?

<!-- notecardId: 1764576530492 -->

```console 
kubectl apply -f pod.yml 
```

## How does a ReplicaSet yml file look like?

<!-- notecardId: 1764576530494 -->

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

## Can ReplicaSets apply to pods already created?

<!-- notecardId: 1764576530497 -->

yes, through the selector

## What are two commands you can use to increase the number of pods in a replicat set without modifying the yml definition file?

<!-- notecardId: 1764576530499 -->

```console
kubectl scale --replicas=6 -f repset.yml
kubectl scale --replicas=6 replicaset myapp-repset
```

## What is the difference between replace and apply?

<!-- notecardId: 1764576530505 -->

replace completely replaces the existing resource, it needs a complete spec
apply can work with a partial spec, as it can also patch an existing resource, not only create a new one

## What does a deployment do?

<!-- notecardId: 1764576530508 -->

manages pod replication through ReplicaSets, provides rolling updates and rollbacks

## How does a deployment yml file look like?

<!-- notecardId: 1764576530513 -->

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

<!-- notecardId: 1764576530515 -->

```console
kubectl get all
```

## Create an nginx pod.

<!-- notecardId: 1764576530517 -->

```console
kubectl run nginx --image=nginx
```

## Generate a pod yaml file without creating it.

<!-- notecardId: 1764576530520 -->

```console
kubectl run nginx --image=nginx --dry-run=client -o yaml > nginx_pod.yaml
```

## Generate a deployment yaml file without creating it.

<!-- notecardId: 1764576530522 -->

```console
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx_deployment.yaml
```

## What does a service do?

<!-- notecardId: 1764576530524 -->

exposes an application behind a single outward-facing endpoint, even when the workload is split across multiple pods

## How does a nodeport service yml file look like?

<!-- notecardId: 1764576530526 -->

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
      nodePort: 30008
```

## What does node port service do?

<!-- notecardId: 1764576530529 -->

maps a specific node port (e.g., 30008) to the target port on your Pod (e.g., 80)
provides external access while keeping internal port targeting intact

## What is the valid range for node port?

<!-- notecardId: 1764576530531 -->

30000-32767

## Which parameter is mandatory from the ports section of the yaml file for node port?

<!-- notecardId: 1764576530534 -->

port

## What are the default values of nodePort and target port when only port parameter is specified in the yaml config of a node port?

<!-- notecardId: 1764576530536 -->

targetPort will have same value as port
nodePort will be a free port in the range of 30000-32767

## Is a NodePort service restricted to running on a single node?

<!-- notecardId: 1764576530538 -->

NO, a NodePort service runs by default across all nodes in the cluster

## What alogrithm does NodePort service use for load balancing?

<!-- notecardId: 1764576530541 -->

random

## What does a ClusterIP service do?

<!-- notecardId: 1764576530543 -->

it groups related pods under the same serivce and ip

## How does a ClusterIP service yml file look like?

<!-- notecardId: 1764576530545 -->

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

## Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379 (with create service).

<!-- notecardId: 1764576530550 -->

```console
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml 
```
(This will not use the pods labels as selectors, instead, it will assume selectors as app=redis)

## What does a LoadBalancer service do?

<!-- notecardId: 1764576530555 -->

exposes the Service externally using an external load balancer (K8s does not directly offer a load balancing component, you must provide one, or use a cloud provider one)

## How does a LoadBalancer service yml file look like in a supported cloud provider?

<!-- notecardId: 1764576530559 -->

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

<!-- notecardId: 1764576530563 -->

it helps organize and isolate resources in your cluster

## What are the three namespaces created at startup?

<!-- notecardId: 1764576530566 -->

kube-system
default
kube-public

## How can a pod in one namespace reach another pod in a different namespace?

<!-- notecardId: 1764576530569 -->

by adding the other namespace to the other pod dns 
same namespace ex: mysql.connect("db-service")
diff namespace ex(namespace dev): mysql.connect("db-service.dev.svc.cluster.local")

## What is used to limit consumption of hardware resources in namespaces?

<!-- notecardId: 1764576530572 -->

ResourceQuota

## How does a ResourceQuota yaml file look like?

<!-- notecardId: 1764576530575 -->

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

<!-- notecardId: 1764576530577 -->

service name : db-service
namespace : dev
subdomain for service : svc
domain : cluster.local

## List all pods in the kube-system namespace.

<!-- notecardId: 1764576530580 -->

```console
kubectl get pods --namespace=kube-system
```

## In what section of the yaml file can you specify the namespace?

<!-- notecardId: 1764576530582 -->

metadata

## How does a namespace yaml file look like?

<!-- notecardId: 1764576530584 -->

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

## How can you set the default namespace for other cli commands to dev?

<!-- notecardId: 1764576530586 -->

```console
kubectl config set-context $(kubectl config current-context) --namespace=dev
```

## List pods in all namespaces.

<!-- notecardId: 1764576530589 -->

```console
kubectl get pods --all-namespaces
```

## What is the difference between the apply and replace kubectl command?

<!-- notecardId: 1764576530592 -->

apply will create if object doesn't exist and update if it exists
update will fail with error if object already exists

## Create a Service named nginx of type NodePort to expose pod nginx’s port 80 on port 30080 (with expose pod).

<!-- notecardId: 1764576530594 -->

```console
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
```
(This will automatically use the pod’s labels as selectors, but you cannot specify the node port)

## What does kubectl explain command do?

<!-- notecardId: 1764576530597 -->

```console
kubectl explain pods
```
provides the yaml fields that can be filled in for a type of api resource
```console
kubectl explain pods.spec
```
provide the yaml fields that can be filled in under a particular section

## List all the fields you can fill in a yaml file for the pod resource.

<!-- notecardId: 1764576530599 -->

```console
kubectl explain pods --recursive
```

## What does the kubectl api-resources command do?

<!-- notecardId: 1764576530602 -->

list the names and short names of all api resources you can manage in k8s

## Deploy a redis pod using the redis:alpine image with the labels tier=db (imperative).

<!-- notecardId: 1764576530604 -->

```cmd
kubectl run redis --image=redis:alpine --labels="tier=db"
```

## Create a service named redis-service to expose the existing redis pod within the cluster on port 6379.

<!-- notecardId: 1764576530606 -->

```cmd
kubectl expose pod redis --type=ClusterIP --name=redis-se
rvice  --port=6379
```

## Create a deployment named webapp using the image kodekloud/webapp-color with 3 replicas.

<!-- notecardId: 1764576530609 -->

```console
kubectl create deployment  webapp --image=kodekloud/webapp-color --replicas=3
```

## What is the default service created when using --port and --expose flags with kubectl run command?

<!-- notecardId: 1764957343553 -->

clusterip

## What are the two config locations that are compared when running kubectl apply and where is it saved?

<!-- notecardId: 1764957343557 -->

local file
live object configuration
last applied configuration

## Why it's not a good ideea to combine imperative and declarative commands?

<!-- notecardId: 1764957343560 -->

imperative commands do not store last applied configuration

## Can you manualy schedule a pod to a specific node if you don't have a scheduler runing?

<!-- notecardId: 1764957343562 -->

yes via the nodeName setting in the spec section

## Get the deails of pods with the label app=App1.

<!-- notecardId: 1764957343565 -->

```console
kubctl get pods --selector app=App1
kubctl get pods -l app=App1
```

## What two factors determine whether a pod can run on a node?

<!-- notecardId: 1764957343568 -->

the taint applied on the node
the pod's toleration for that taint

## Taint node1 so that it only accepts pods associated with the application blue.

<!-- notecardId: 1764957343571 -->

```console
kubectl taint nodes node1 app=blue:NoSchedule
```

## What are the three taint effects?

<!-- notecardId: 1764957343573 -->

NoSchedule
PreferNoSchedule
NoExecute

## What does the NoSchedule taint effect do?

<!-- notecardId: 1764957343576 -->

pods that do not tolerate the taint 
will not be scheduled on the node

## What does the PreferNoSchedule taint effect do?

<!-- notecardId: 1764957343579 -->

the scheduler tries to avoid placing non-tolerating pods on the node, 
but it is not strictly enforced

## What does the NoExecute taint effect do?

<!-- notecardId: 1764957343582 -->

new pods without a matching toleration will not be scheduled 
existing pods without a matching toleration will be evicted from the node

## How does the tolerations section of a yaml pod spec look like?

<!-- notecardId: 1764957343585 -->

```yaml
spec:
  containers:
    - name: nginx-container
      image: nginx
  tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
```

## Remove the taint on node1 (it only accepts pods associated with the application blue).

<!-- notecardId: 1764957343588 -->

```console
kubectl taint nodes node1 app=blue:NoSchedule-
```
## Label node1 with size=large.

<!-- notecardId: 1764957343591 -->

```console
kubectl label nodes node1 size=large
```

## How does pod yaml with a node selector look like?

<!-- notecardId: 1765219979196 -->

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: data-processor
      image: data-processor
  nodeSelector:
    size: Large
```

## How does a pod yaml with node afinity look like?

<!-- notecardId: 1765219979200 -->

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: data-processor
      image: data-processor
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: size
                operator: In
                values:
                  - Large
```

## What are the four operators usable in node afinity?

<!-- notecardId: 1765219979204 -->

In, NotIn, Exists, DoesNotExist

## What are the two types of node afinity

<!-- notecardId: 1765219979207 -->

requiredDuringSchedulingIgnoredDuringExecution
the scheduler can't schedule the Pod unless the rule is met
preferredDuringSchedulingIgnoredDuringExecution
the scheduler tries to find a node that meets the rule
if a matching node is not available, the scheduler still schedules the Pod

## When should you use taints and tolerations vs node afinity and labels?

<!-- notecardId: 1765219979211 -->

taints prevent other pods from running on your nodes 
afinity prevent your pods from running on other nodes
if you need to run only certain pods on certain nodes 
a combination of both needs to be used

## What does a pod yaml file with resource requirements and limits look like?

<!-- notecardId: 1765219979215 -->

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
  labels:
    name: simple-webapp-color
spec:
  containers:
  - name: simple-webapp-color
    image: simple-webapp-color
    ports:
    - containerPort: 8080
    resources:
      requests:
        memory: "4Gi"
        cpu: 2
      limits:
        memory: "2Gi"
        cpu: 2
```

## How manny bytes is a gigabyte(GB)?

<!-- notecardId: 1765219979219 -->

10 to the power of 9

## How manny bytes is a gibibyte(Gi)?

<!-- notecardId: 1765219979222 -->

2 to the power of 30

## Can you used fractional cpu, if so, in what interval?

<!-- notecardId: 1765219979226 -->

yes from 1m (1mili) to 1000m (1cpu), 0.1cpu is 100m

## What does cpu refer to when used as resource requirement?

<!-- notecardId: 1765219979230 -->

1 aws vcpu
1 gcp/azure core
1 hyperthread in other platforms

## How does a yaml file definition of limit range for cpu look like?

<!-- notecardId: 1765219979233 -->

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-resource-constraint
spec:
  limits:
    - default:
        cpu: 500m
      defaultRequest:
        cpu: 500m
      max:
        cpu: "1"
      min:
        cpu: 100m
      type: Container
```

## How does a yaml file definition of limit range for memory look like?

<!-- notecardId: 1765219979237 -->

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: memory-resource-constraint
spec:
  limits:
    - default:
        memory: 1Gi
      defaultRequest:
        memory: 1Gi
      max:
        memory: 1Gi
      min:
        memory: 500Mi
      type: Container
```

## Will a limit range affect existing pods?

<!-- notecardId: 1765219979241 -->

no, only newly created or updated pods

## What can be created at a namespace level to manage resource consumption?

<!-- notecardId: 1765219979245 -->

resource quotas

## How does a resource quota yaml file look like for memory and cpu?

<!-- notecardId: 1765219979248 -->

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-resources
spec:
  hard:
    requests.cpu: "1"
    requests.memory: "1Gi"
    limits.cpu: "2"
    limits.memory: "2Gi"
    requests.nvidia.com/gpu: 4
```

## How do you extract the yaml definition of an existing object?

<!-- notecardId: 1765219979252 -->

```console
kubectl get pod webapp -o yaml > ex_pod.yaml
```

## What do daemon sets do?

<!-- notecardId: 1765219979255 -->

ensure that exactly one copy of a pod runs on every node in your Kubernetes cluster

## How does a DaemonSet yaml file look like?

<!-- notecardId: 1765219979261 -->

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: monitoring-daemon
spec:
  selector:
    matchLabels:
      app: monitoring-agent
  template:
    metadata:
      labels:
        app: monitoring-agent
    spec:
      containers:
        - name: monitoring-agent
          image: monitoring-agent
```

## How do you get one type of resources from all namespaces?

<!-- notecardId: 1765219979264 -->

```console
kubectl get pods --all-namespaces
```

## What is the fastest way to generate a daemonset yaml?

<!-- notecardId: 1765219979268 -->

create a deployment, replace kind with daemonset and remove strategy and replicas

## What is a usecase for static pods?

<!-- notecardId: 1765219979272 -->

creating the control plane components

## What is ignored by kube-scheduler by default?

<!-- notecardId: 1765219979275 -->

static pods and daemon sets

## List all static pods in all namespaces.

<!-- notecardId: 1765219979279 -->

```console
k get pods --all-namespaces -o custom-columns=NAME:.metadata.name,OWNER:.metadata.ownerReferences[].kind
```
the owner reference for static pods is "Node"

## How do you see what pods are running on what node?

<!-- notecardId: 1765219979283 -->

```console
kubectl get pods --all-namespaces -o wide
```

## Create a static pod named static-busybox that uses the busybox image , run in the default namespace and the command sleep 1000.

<!-- notecardId: 1765219979286 -->

```console
kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```

## Where is the kubelet config file?

<!-- notecardId: 1765219979290 -->

```console
/var/lib/kubelet/config
```

## What is the apps priority range?

<!-- notecardId: 1765219979294 -->

from 1 000 000 000 to around -2 000 000 000

## What is the system priority range?

<!-- notecardId: 1765219979298 -->

from 2 000 000 000 to 1 000 000 000

## How does a PriorityClass yaml look like?

<!-- notecardId: 1765219979301 -->

```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
value: 1000000000
description: "Priority class for mission critical pods"
preemptionPolicy: PreemptLowerPriority
```

## What are the two preemption policies and what do they do?

<!-- notecardId: 1765219979305 -->

PreemptLowerPriority
will kill and replace lower prio pods 
Never
will wait for existing pods to finish
order in que is still based on the priority


## How does a custom scheduler yaml look like?

<!-- notecardId: 1765268662588 -->

```yaml
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profiles:
  - schedulerName: my-scheduler
```

## How do you create a config map for a custom scheduler?

<!-- notecardId: 1765268662591 -->

```console
kubectl create configmap my-scheduler-config --from-file=path/to/kubeScheduler/config/file.yaml --namespace kube system
```

## What are the three ways you can deploy a scheduler?

<!-- notecardId: 1765268662593 -->

as a binary
as a pod
as a deployment

## How does a custom scheduler pod yaml file look like?

<!-- notecardId: 1765268662596 -->

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-custom-scheduler
  namespace: kube-system
spec:
  containers:
    - name: kube-scheduler
      image: k8s.gcr.io/kube-scheduler-amd64:v1.11.3
      command:
        - kube-scheduler
        - --address=127.0.0.1
        - --kubeconfig=/etc/kubernetes/scheduler.conf
        - --config=/etc/kubernetes/my-scheduler-config.yaml
```

## How do you configure a pod to use a custom scheduler?

<!-- notecardId: 1765268662599 -->

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
    - name: nginx
      image: nginx
  schedulerName: my-custom-scheduler
```

## How can you see what scheduler picked up a certain pod?

<!-- notecardId: 1765268662601 -->

```console
kubectl get events -o wide
```

## How can you view the logs of my-custom-scheduler in the kube-system namespace?

<!-- notecardId: 1765268662604 -->

```console
kubectl logs my-custom-scheduler --namespace=kube-system
```

## Describe how pod scheduling happens and what plugins are used?

<!-- notecardId: 1765268662607 -->

scheduling que -> PrioritySort
filtering nodes -> NodeResourceFit/NodeName
scoring of nodes -> NodeResourceFit/ImageLocality 
binding the pod to the node with the highest score -> DefaultBinder 

## Configure a custom schedulers my-scheduler-2, that replaces the score default TaintToleration plugin with two custom plugins MyCustomPluginA and MyCustomPluginB.

<!-- notecardId: 1765268662609 -->

```yaml
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profiles:
  - schedulerName: my-scheduler-2
    plugins:
      score:
        disabled:
          - name: TaintToleration
        enabled:
          - name: MyCustomPluginA
          - name: MyCustomPluginB
```

## Configure a custom schedulers my-scheduler-3, that disables all the prescore and score plugins.

<!-- notecardId: 1765268662612 -->

```yaml
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profiles:
  - schedulerName: my-scheduler-3
    plugins:
      preScore:
        disabled:
          - name: '*'
      score:
        disabled:
          - name: '*'
```

## What are the steps a kubelet takes before creating a pod?

<!-- notecardId: 1765268662614 -->

authentication
authorization
addmission controller

## Check what admission controllers are enabled.

<!-- notecardId: 1765268662617 -->

```console
kube-apiserver -h | grep enable-admission-plugins
```

## What does the AlwaysPullImages admission controller do?

<!-- notecardId: 1765268662619 -->

forces image pulling on each pod creation

## What does the DefaultStorageClass admission controller do?

<!-- notecardId: 1765268662621 -->

automatically assigns a default storage class to PVCs if none is specified

## What does the EventRateLimit admission controller do?

<!-- notecardId: 1765268662624 -->

limits the number of concurrent API server requests to prevent overload

## What does the NamespaceExists admission controller do?

<!-- notecardId: 1765268662626 -->

Rejects requests to operate in non-existent namespaces.

## Where can you enable/dissable extra admission controllers?

<!-- notecardId: 1765268662629 -->

in /etc/kubernetes/manifests/kube-apiserver.yaml 
enable-admission-plugins=some-other-admission-controller
disable-admission-plugins=some-default-admission-controller

## What are the three types of admission controllers?

<!-- notecardId: 1765268662631 -->

mutating, that modifies the incomming request 
validating, that just checks if a condition is met
dual-purpose, that do both

## In what order are the single purpose admission controllers run?

<!-- notecardId: 1765268662633 -->

mutating
validating

## How can you implement admission controller logic external to kubernetes?

<!-- notecardId: 1765268662638 -->

through a implementing an admission webhook server 
and creating a web hook configuration on the cluster that will forward admission requests to the server

## Create a tls secret in the webhok-demo namespace.

<!-- notecardId: 1765268662641 -->

```console
kubectl -n webhook-demo create secret tls webhook-server-tls
```

<!-- log and monitoring -->


