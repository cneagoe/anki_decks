# cka

## What are the main components of the control plane?

etcd
scheduler
controllers
api server

## What does etcd do?

stores cluster-wide configuration and state data in a key-value store

## What does the scheduler do?

determines the best node for new pods deployments

## What is a controller?

a control loop that watches the state of your cluster and makes or requests changes where needed

## What does the api server do?

acts as the central hub for cluster communication and management

## What is the difference between key-value store and relational data bases?

does not require a schema
has no support for complex queries
has verry good performance
is very flexible
is best used for simple fast lookup

## What is the default port for etcd?

2379

## In a high availability environment how do the multiple etcd instances know about each other?

through the initial-cluster config setting

## Where can you see the settings of each pod from the kube-system namespace?

```console
/etc/kubernetes/manifest/
```

## Where can you find the services of the main control plane components?

```console
/etc/systemd/system/kube-controller-manager.service
```

## What are the main components of the worker nodes?

kubelet
kube proxy
pod

## What is the role of the kubelet?

takes the PodSpecs provided and ensures that the containers described in those PodSpecs are running and healthy

## What is the kube proxy?

runs in a pod on every node in the Kubernetes cluster
monitors for Service creations and configure network rules that redirect traffic to the corresponding pods

## What does a replica set do?

ensures high availability by creating and maintaining the desired number of pod replicas
it spans across multiple nodes on the cluster

## What is the difference between replicaSet and replication controller?

replica set is the new way of managing pod replication
replication controller is the old way

## Can ReplicaSets apply to pods already created?

yes, through the selector

## What is the difference between replace and apply?

replace completely replaces the existing resource, it needs a complete spec
apply can work with a partial spec, as it can also patch an existing resource, not only create a new one

## What does a deployment do?

manages pod replication through ReplicaSets, provides rolling updates and rollbacks

## What does a service do?

exposes an application behind a single outward-facing endpoint, even when the workload is split across multiple pods

## What does node port service do?

maps a specific node port (e.g., 30008) to the target port on your Pod (e.g., 80)
provides external access while keeping internal port targeting intact

## What is the valid range for node port?

30000-32767

## Which parameter is mandatory from the ports section of the yaml file for node port?

port

## What are the default values of nodePort and target port when only port parameter is specified in the yaml config of a node port?

targetPort will have same value as port
nodePort will be a free port in the range of 30000-32767

## Is a NodePort service restricted to running on a single node?

NO, a NodePort service runs by default across all nodes in the cluster

## What alogrithm does NodePort service use for load balancing?

random

## What does a ClusterIP service do?

it groups related pods under the same serivce and ip

## What does a LoadBalancer service do?

exposes the Service externally using an external load balancer (K8s does not directly offer a load balancing component, you must provide one, or use a cloud provider one)

## What does a namespace do?

it helps organize and isolate resources in your cluster

## What are the three namespaces created at startup?

kube-system
default
kube-public

## How can a pod in one namespace reach another pod in a different namespace?

by adding the other namespace to the other pod dns 
same namespace ex: mysql.connect("db-service")
diff namespace ex(namespace dev): mysql.connect("db-service.dev.svc.cluster.local")

## What is used to limit consumption of hardware resources in namespaces?

ResourceQuota

## Given the following dns service name db-service.dev.svc.cluster.local, explain the name components.

service name : db-service
namespace : dev
subdomain for service : svc
domain : cluster.local

## In what section of the yaml file can you specify the namespace?

metadata

## What is the difference between the apply and replace kubectl command?

apply will create if object doesn't exist and update if it exists
update will fail with error if object already exists

## What is the default service created when using --port and --expose flags with kubectl run command?

clusterip

## What are the two config locations that are compared when running kubectl apply and where is it saved?

local file
live object configuration
last applied configuration

## Why it's not a good ideea to combine imperative and declarative commands?

imperative commands do not store last applied configuration

## Can you manualy schedule a pod to a specific node if you don't have a scheduler runing?

yes via the nodeName setting in the spec section

## What two factors determine whether a pod can run on a node?

the taint applied on the node
the pod's toleration for that taint

## What are the three taint effects?

NoSchedule
PreferNoSchedule
NoExecute

## What does the NoSchedule taint effect do?

pods that do not tolerate the taint 
will not be scheduled on the node

## What does the PreferNoSchedule taint effect do?

the scheduler tries to avoid placing non-tolerating pods on the node, 
but it is not strictly enforced

## What does the NoExecute taint effect do?

new pods without a matching toleration will not be scheduled 
existing pods without a matching toleration will be evicted from the node

## What are the four operators usable in node afinity?

In, NotIn, Exists, DoesNotExist

## What are the two types of node afinity

requiredDuringSchedulingIgnoredDuringExecution
the scheduler can't schedule the Pod unless the rule is met
preferredDuringSchedulingIgnoredDuringExecution
the scheduler tries to find a node that meets the rule
if a matching node is not available, the scheduler still schedules the Pod

## When should you use taints and tolerations vs node afinity and labels?

taints prevent other pods from running on your nodes 
afinity prevent your pods from running on other nodes
if you need to run only certain pods on certain nodes 
a combination of both needs to be used

## How manny bytes is a gigabyte(GB)?

10 to the power of 9

## How manny bytes is a gibibyte(Gi)?

2 to the power of 30

## Can you used fractional cpu, if so, in what interval?

yes from 1m (1mili) to 1000m (1cpu), 0.1cpu is 100m

## What does cpu refer to when used as resource requirement?

1 aws vcpu
1 gcp/azure core
1 hyperthread in other platforms

## Will a limit range affect existing pods?

no, only newly created or updated pods

## What can be created at a namespace level to manage resource consumption?

resource quotas

## How do you extract the yaml definition of an existing object?

```console
kubectl get pod webapp -o yaml > ex_pod.yaml
```

## What do daemon sets do?

ensure that exactly one copy of a pod runs on every node in your Kubernetes cluster

## How does a DaemonSet yaml file look like?

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

```console
kubectl get pods --all-namespaces
```

## What is the fastest way to generate a daemonset yaml?

create a deployment, replace kind with daemonset and remove strategy and replicas

## What is a usecase for static pods?

creating the control plane components

## What is ignored by kube-scheduler by default?

static pods and daemon sets

## List all static pods in all namespaces.

```console
k get pods --all-namespaces -o custom-columns=NAME:.metadata.name,OWNER:.metadata.ownerReferences[].kind
```
the owner reference for static pods is "Node"

## How do you see what pods are running on what node?

```console
kubectl get pods --all-namespaces -o wide
```

## Create a static pod named static-busybox that uses the busybox image , run in the default namespace and the command sleep 1000.

```console
kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```

## Where is the kubelet config file?

```console
/var/lib/kubelet/config
```

## What is the apps priority range?

from 1 000 000 000 to around -2 000 000 000

## What is the system priority range?

from 2 000 000 000 to 1 000 000 000

## How does a PriorityClass yaml look like?

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

PreemptLowerPriority
will kill and replace lower prio pods 
Never
will wait for existing pods to finish
order in que is still based on the priority


## How does a custom scheduler yaml look like?

```yaml
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profiles:
  - schedulerName: my-scheduler
```

## How do you create a config map for a custom scheduler?

```console
kubectl create configmap my-scheduler-config --from-file=path/to/kubeScheduler/config/file.yaml --namespace kube system
```

## What are the three ways you can deploy a scheduler?

as a binary
as a pod
as a deployment

## How does a custom scheduler pod yaml file look like?

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

```console
kubectl get events -o wide
```

## How can you view the logs of my-custom-scheduler in the kube-system namespace?

```console
kubectl logs my-custom-scheduler --namespace=kube-system
```

## Describe how pod scheduling happens and what plugins are used?

scheduling que -> PrioritySort
filtering nodes -> NodeResourceFit/NodeName
scoring of nodes -> NodeResourceFit/ImageLocality 
binding the pod to the node with the highest score -> DefaultBinder 

## Configure a custom schedulers my-scheduler-2, that replaces the score default TaintToleration plugin with two custom plugins MyCustomPluginA and MyCustomPluginB.

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

authentication
authorization
addmission controller

## Check what admission controllers are enabled.

```console
kube-apiserver -h | grep enable-admission-plugins
```

## What does the AlwaysPullImages admission controller do?

forces image pulling on each pod creation

## What does the DefaultStorageClass admission controller do?

automatically assigns a default storage class to PVCs if none is specified

## What does the EventRateLimit admission controller do?

limits the number of concurrent API server requests to prevent overload

## What does the NamespaceExists admission controller do?

Rejects requests to operate in non-existent namespaces.

## Where can you enable/dissable extra admission controllers?

in /etc/kubernetes/manifests/kube-apiserver.yaml 
enable-admission-plugins=some-other-admission-controller
disable-admission-plugins=some-default-admission-controller

## What are the three types of admission controllers?

mutating, that modifies the incomming request 
validating, that just checks if a condition is met
dual-purpose, that do both

## In what order are the single purpose admission controllers run?

mutating
validating

## How can you implement admission controller logic external to kubernetes?

through a implementing an admission webhook server 
and creating a web hook configuration on the cluster that will forward admission requests to the server

## Create a tls secret in the webhok-demo namespace.

```console
kubectl -n webhook-demo create secret tls webhook-server-tls
```

## How can you check resource consumption of nodes?

```console
kubectl top node
```

## How can you check the logs of a pod in real time?

```console
kubectl logs -f pod-name
```

## What is the default deployment strategy?

rolling update

## How can you rollback a deployment?

```console
kubectl rollout undo deployment/myapp-deployment
```

## How can you check the history of a deployment?

```console
kubectl rollout history deployment/myapp-deployment
```

## How can you change the image version of a container in a deployment without changing the yaml file(imperative)?

```console
kubectl set image deployment myapp-deployment nginx=nginx:1.9.1
```

## How can you check the status of a deployment?

```console
kubectl rollout status deployment myapp-deployment
```

## What do the command and args fields from a container spec correspond to in docker?

command -> entrypoint
args -> cmd

## What is the best format to pass commands to a container?

json array 
```json
["some_command","arg1","arg2"]
```

## How does a yaml pod definition that overrides the entrypoint and cmd settings of the image?

```yaml
apiVersion: v1
kind: Pod 
metadata:
  name: webapp-green
  labels:
      name: webapp-green
spec:
  containers:
  - name: simple-webapp
    image: kodekloud/webapp-color
    command: ["python", "app.py"]
    args: ["--color", "pink"]
```

## How does a pod yaml config with environment variables look like?

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
spec:
  containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      ports:
        - containerPort: 8080
      env:
        - name: APP_COLOR
          value: pink
```

## How does the yaml file for ConfigMap look like?

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: blue
  APP_MODE: prod
```

## How does a pod that uses a config map look like?

```yaml 
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
spec:
  containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      ports:
        - containerPort: 80
      envFrom:
        - configMapRef:
            name: app-color
```

## How does a yaml pod config look like where only one env var is taken from the config map?

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: webapp-color
  name: webapp-color
  namespace: default
spec:
  containers:
  - env:
    - name: APP_COLOR
      valueFrom:
       configMapKeyRef:
         name: webapp-config-map
         key: APP_COLOR
    image: kodekloud/webapp-color
    name: webapp-color
```

## How do you encode a string in base64?

```console
echo -n 'somepass' | base64
```

## How do you decode a string in base64?

```console
echo -n 'cm9vdA==' | base64 --decode
```

## How does a secret yaml config file look like?

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
data:
  DB_Host: bXlzcWw=
  DB_User: cm9vdA==
  DB_Password: cGFzd3Jk
```

## What is used in a secret file to prevent having a password in clear text?

base64 encoding

## How does a yaml file for a pod using a secret look like?

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
    envFrom:
    - secretRef:
        name: app-secret
```

## How does a volumes yaml config that uses secrets look like?

```yaml
volumes:
- name: app-secret-volume
  secret:
    secretName: app-secret
```

## How are secrets stored in volume that uses them?

in files
the filename is the key
the contents are the secret

## Will secrets created before enabling encription at rest on etcd be vissible in clear text after?

yes, encryptions only covers new objects
you will need to recreate old secrets

## How does an init container pod yaml config look like?

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app.kubernetes.io/name: MyApp
spec:
  containers:
  - name: myapp-container
    image: busybox:1.28
    command: ['sh', '-c', 'echo The app is running! && sleep 3600']
  initContainers:
  - name: init-myservice
    image: busybox:1.28
    command: ['sh', '-c', "until nslookup myservice.$(cat /var/run/secrets/kubernetes.io/serviceaccount/namespace).svc.cluster.local; do echo waiting for myservice; sleep 2; done"]
  - name: init-mydb
    image: busybox:1.28
    command: ['sh', '-c', "until nslookup mydb.$(cat /var/run/secrets/kubernetes.io/serviceaccount/namespace).svc.cluster.local; do echo waiting for mydb; sleep 2; done"]
```

## How does a sidecar container pod yaml config look like?

```yaml
spec:
  containers:
    - name: myapp
      image: alpine:latest
      command: ['sh', '-c', 'while true; do echo "logging" >> /opt/logs.txt; sleep 1; done']
      volumeMounts:
        - name: data
          mountPath: /opt
  initContainers:
    - name: logshipper
      image: alpine:latest
      restartPolicy: Always
      command: ['sh', '-c', 'tail -F /opt/logs.txt']
      volumeMounts:
        - name: data
          mountPath: /opt
```

## Execute the cat /log/app.log command in the app pod.

```console
kubectl exec -it app -- cat /log/app.log
```

## What does the scale command do?

adjust the number of replicas in a deployment or replicaset

## Can the scale command be used to scale down a statefullset in kubernetes?

yes it can scale both deployments and statefullset

## If you scale a deployment using kubectl scale to a higher number of replicas, but the cluster has insufficient resources to accommodate all new replicas, what will happen?

as manny replicas as possible will be created with the existing resources, the rest of the replicas will keep the deployment in a pending state until there are sufficient resources for all

## How does a HorizontalPodAutoscaler yaml config look like?

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  creationTimestamp: null
  name: nginx-deployment
spec:
  maxReplicas: 3
  metrics:
  - resource:
      name: cpu
      target:
        averageUtilization: 80
        type: Utilization
    type: Resource
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment
status:
  currentMetrics: null
  desiredReplicas: 0
  currentReplicas: 0
```

## What is the primary purpose of the Horizontal Pod Autoscaler (HPA) in Kubernetes?

to automate the creation of new pods based on consumption of certain resources

## What component in a Kubernetes cluster is responsible for providing metrics to the HPA?

metrics-server

## The HPA status shows /80 for the CPU target. what could be a possible reason?

the deployment does not have any resource fields defined

## What does the event ScalingReplicaSet in the nginx-deployment HPA indicate?

the hpa is increasing the nr of pods

## What is a possible cause for FailedGetResourceMetric event in the nginx-deployment HPA?

cpu or memory requests are missing for a container

## From what kubernetes version on is the in-place pod resizing feature enabled by default?

1.33

## What env var determines if InPlaceVerticalScaling is enabled?

```console
FEATURE_GATES=InPlacePodVerticalScaling=true
```

## How does a deploment spec section where inplace vert scaling is enabled?

``` yaml
spec:
  containers:
  - name: my-app
    image: nginx
    resizePolicy:
      - resourceName: cpu
        restartPolicy: NotRequired
    resources:
      requests:
        cpu: "250m"
        memory: "256Mi"
      limits:
        cpu: "500m"
        memory: "512Mi"
```

## What types of resources does inplace vert scaling support?

ram, cpu

## What are the components of VPA(VerticalPodAutoscaler)?

vpa admission controller
vpa updater
vpa recommender

## Which VPA component communicates with the metrics server?

vpa recommender

## Which VPA component is in charge of the pod eviction?

vpa updater

## Which VPA component is in charge of creating new pods?

vpa admission controller

## How does a VerticalPodAutoscaler yaml config look like?

```yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: my-app-vpa
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  updatePolicy:
    updateMode: "Auto"
  resourcePolicy:
    containerPolicies:
      - containerName: "my-app"
        minAllowed:
          cpu: "250m"
        maxAllowed:
          cpu: "2"
        controlledResources: ["cpu"]
```

## What will be the behavior of a vpa with updateMode: Off?

it will only recommend and not actualy change anything
updater and admission controller ore off

## What will be the behavior of a vpa with updateMode: Initial?

it will only change pods on creation and not later on
updater is off

## What will be the behavior of a vpa with updateMode: Recreate?

pods will be evicted and recreated if the consumption threshold is reached

## What will be the behavior of a vpa with updateMode: Auto?

same as recreate but should support in place resizing in the future
As of Kubernetes 1.34, VPA does not support resizing pods in-place, but this integration is in progress

## How can you see info about a vpa?

```console
kubectl describe vpa my-vpa
```

## What types of workload is vpa best for?

stateful workloads, databases, JVM-based applications, and AI workloads requiring precise tuning

## What types of workload is hpa best for?

stateless applications, web services, and microservices requiring rapid scaling

## What happens when you have only 1 replica and VPA tries to evict it?

Kubernetes blocks this action with the error message: "too few replicas".

## Where is the pod eviction timeout set?

on the controller manager 

## What is the default value of the eviction timeout?

5min

## How can you empty a node of pods?

```console
kubectl drain node-1
```

## What does draining a node do?

kills all pods on that node and recreates them on the rest of the nodes

## What is needed after draining a node so that pods can be scheduled on it again?

```console
kubectl uncordon node-1
```

## How can you blok a node from getting new pods scheduled on it?

```console
kubectl cordon node-1
```

## How much of a difference in version nr can there be between k8s components?

if kube-apiserver is version x
controller-manager and kube-scheduler can be x-1
kubelet and kube-proxy can be x-2
kubectl can be from x+1 to x-1

## Is it better to update from 1.10 to 1.15 directly or do all the intermediary versions?

the best practice is to do one version at a time 1.10 to 1.11, 1.11 to 1.12 and so on

## How can you see what the current component versions are if your cluster was set up with kubeadm?

```console
kubeadm upgrade plan
```

## How can you update the version of k8s control components (except kubelet) with kubeadm?

```console
kubeadm upgrade apply v1.34
```

## What needs to be done before and after upgrading kubelet?
before
```console
kubectl drain node
```
after
```console
systemctl restart kubelet
kubectl uncordon node
```

## How can you get a config yaml for the entire cluster?

```console
kubectl get all --all-namespaces -o yaml > bk.yaml
```

## What param in the etcd config contains the backup location?

```console
--data-dir=/var/lib/etcd
```

## Create an etcd snapshot called "snapshot.db using etcdctl"

```console
ETCDCTL_API=3 etcdctl --endpoints=https://[127.0.0.1]:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/snapshot-pre-boot.db
```

## Restore an etcd snapshot called "snapshot.db" using etcdctl with the data-dir in a different location.

```console
etcdutl snapshot restore /opt/snapshot.db --data-dir /var/lib/etcd-from-backup
```

## What is left to do after restoring a snapshot of etcd from backup?

modify the manifest so that it points to the new data-dir location

## Get more info on etcd backups.

```console
etcdctl snapshot status
```

## How do you perform a raw file-level copy of etcd’s data and WAL files without needing etcd running

```console
etcdutl backup
```

## List all containers with crictl.

```console
crictl ps -a
```

## What types of accounts can be managed in k8s?

service accounts, user accounts need be managed via third party (ldap, kerberos, etc)

## Generate a private tls key.

```console
openssl genrsa -aut my-bank.key 1024
```

## Generate a public tls key.

```console
openssl rsa -in my-bank.key -pubout > mybank.pem
```

## What is the difference between ssl and tls?

ssl (old security protocol)
secure sockets layer
tls (new security protocol)
transport level security

## Create a local certificate authority (CA).

```console
openssl genrsa -out ca.key 2048
openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr
openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
```

## What steps are needed to create a CA?

create a CA key (ca.key)
use the key to create a certificate sign request (ca.csr)
use the key and csr to create the certificate (ca.crt)

## View the details of /etc/kubernetes/pki/apiserver.crt

```console
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
```

## Show logs of the etcd.service

```console
journalctl -u etcd.service -l
```

## Show logs of the etcd-master pod

```console
kubectl logs etcd-master
```

## show container logs 

```console
crictl ps -a
crictl logs 87fc
```

## How does a yaml file for a CertificateSigningRequest look like?

```yaml
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: akshay
spec:
  groups:
  - system:authenticated
  request: <Paste the base64 encoded value of the CSR file>
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
```

## Approve a CSR request via the api.

```console
kubectl certificate approve akshay
```

## Reject a CSR request via the api.

```console
kubectl certificate deny agent-smith
```

## Completely remove a CSR via the api.

```console
kubectl delete csr agent-smith
```

## How do you execute a date command on a container called ruby-container in a pod called mypod? 

```console
kubectl exec mypod -c ruby-container -- date
```



<!-- kubeConfig  -->