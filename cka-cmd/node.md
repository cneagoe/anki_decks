# cka-cmd

## List all objects in cluster.

```console
kubectl get all
```

## List pods in current default namespace.

```console
kubectl get pods
```

## List all pods in the kube-system namespace.

```console
kubectl get pods -n kube-system
```
## List all pods in all namespaces.

```console
kubectl get pods --all-namespaces
```

## Get the details of pods with the label app=App1.

```console
kubctl get pods -l app=App1
```

## Save the config on an existing nginx pod into a yaml file.

```console
kubectl get pod nginx -o yaml > nginx.yaml
```

## List details about pod called myapp.

```console
kubectl describe pod myapp
```

## Remove a pod called myapp.

```console
kubectl delete pod myapp
```

## How do you execute a yml file(ex: pod.yml) with kubectl?

```console 
kubectl apply -f pod.yml 
```

## Create an nginx pod.

```console
kubectl run nginx --image=nginx
```

## Deploy a redis pod using the redis:alpine image with the labels tier=db (imperative).

```cmd
kubectl run redis --image=redis:alpine --labels="tier=db"
```

## Generate a deployment yaml file for a nginx pod without creating it.

```console
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx_deployment.yaml
```

## Create a deployment named webapp using the image kodekloud/webapp-color with 3 replicas.

```console
kubectl create deployment  webapp --image=kodekloud/webapp-color --replicas=3
```

## Create a Service named redis of type ClusterIP to expose port 6379 on pod redis with the same port.

```console
kubectl create service clusterip redis --tcp=6379:6379 
```
(This will use the pod label "app: redis" as selector)

## Create a yaml file for a Service named nginx-service of type NodePort by exposing pod nginx’s port 80 on port 30080.

```console
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
```
(This will automatically use the pod’s labels as selectors, but you cannot specify the node port)

## Increase the number of pods to 6 in repset.yml.

```console
kubectl scale --replicas=6 -f repset.yml
```

## Increase the number of pods to 6 in replicaset myapp-repset.

```console
kubectl scale --replicas=6 replicaset myapp-repset
```

## Get the name of the current config context.

```console
kubectl config current-context
```

## How can you set the default namespace for other cli commands to dev?

```console
kubectl config set-context $(kubectl config current-context) --namespace=dev
```

## List the supported API resources,(names, shortnames, etc) on the server.

```console
kubectl api-resources
```

## Taint node1 so that it only accepts pods associated with the application blue.

```console
kubectl taint nodes node1 app=blue:NoSchedule
```

## Remove the taint on node1 (it only accepts pods associated with the application blue).

```console
kubectl taint nodes node1 app=blue:NoSchedule-
```

## Label node1 with size=large.

```console
kubectl label nodes node1 size=large
```

## How do you check the etcd version?

```console
etcdctl version
```

## What command shows all keys stored in etcd?

```console
etcdctl get / --prefix --keys-only=true
```

## How do you execute a etcdl command in the etcd-master pod of the kube-system namespace?

```console
kubectl exec etcd-master -n kube-system -- etcdl something
```