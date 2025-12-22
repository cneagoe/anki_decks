# cka-yaml

## What are the required configuration fields for a yml file?

apiVersion
kind
metadata
spec

## Get the documentation for all the fields of a resource (ex. pods).

```console
kubectl explain pods --recursive
```

## Get the documentation of a specific field of a resource (ex. pods spec containers)

```console  
kubectl explain pods.spec.containers
```

## How do you export a live pod (caled mypod) configuration to a local yaml file?

```console
kubectl get pod/mypod -o yaml > mypod.yaml
```

## How does a Pod yaml config look like?

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

## How does the nodeSelector field look like in a pod yaml config?

```yaml
spec:
  nodeSelector:
    size: Large
```

## How does the nodeAfinity field look like in a pod yaml config?

```yaml
spec:
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

## How does the resources field look like in pod yaml config?

```yaml
# other pod config
spec:
  containers:
  - name: simple-webapp-color
    image: simple-webapp-color
    resources:
      requests:
        memory: "4Gi"
        cpu: 2
      limits:
        memory: "2Gi"
        cpu: 2
```

## Delete the status field from nginx.yaml.
```console
 yq -i eval 'del(.status)' nginx.yaml 
```

## Get the value of the image field from the p.yaml pod config file.

```console
yq '.spec.containers[0].image' p.yaml
```

## Change the image in the p.yaml pod config file to nginx.

```console
yq -i '.spec.containers[0].image= "nginx"' p.yaml
```

## How does a ReplicaSet yaml file look like?

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  # name, labels etc
spec:
  replicas: 3
  selector:
    matchLabels:
      type: front-end
  template:
    # metadata and spec from pod
```

## How does a Deployment yaml file look like?

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  # name, labels etc
spec:
  replicas: 3
  selector:
    matchLabels:
      type: front-end
  template:
    # metadata and spec from pod
```

## How does a NodePort service yaml file look like?

```yaml
apiVersion: v1
kind: Service
metadata:
  # name, labels etc
spec:
  type: NodePort
  ports:
    - targetPort: 80
      port: 80
      nodePort: 30008
```

## How does a ClusterIP service yml file look like?

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

## How does a LoadBalancer service yml file look like in a supported cloud provider?

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

## How does a ResourceQuota for memory and cpu yaml file look like?

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

## How does a namespace yaml file look like?

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

## How does the tolerations section of a yaml pod spec look like?

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

## How does a yaml file definition of LimitRange for cpu look like?

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