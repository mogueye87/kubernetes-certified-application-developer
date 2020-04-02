# Labels, selectors and annotations
## Labels
A label is a key-value pairs attached to a kubernetes object. This can be used to select a group of subsets of those object.
We can attached labels to object with `metadata.labels`

the command use to show a label of running pod is : 

`kubectl get pod <pod_name> --show-labels`

**porduction**
```sh
apiVersion: v1
kind: Pod
metadata:
  name: my-production-label
  labels:
    name: my-app
    environment: production
spec:
  containers:
  - name: nginx
    image: nginx
```

**development pod**
```sh
apiVersion: v1
kind: Pod
metadata:
  name: my-production-label
  labels:
    app: my-app
    environment: development
spec:
  containers:
  - name: nginx
    image: nginx
```

## Selectors
> You can use various selectors to select different subsets of objects.
```sh

kubectl get pods -l app=my-app

kubectl get pods -l environment=production

kubectl get pods -l environment=development

kubectl get pods -l environment!=production

kubectl get pods -l 'environment in (development,production)'

kubectl get pods -l app=my-app,environment=production
```

## Annotations
> Another are like labels, they are metadata attached to Kubernetes object.
  However, contrary to labels which can be used to organize, identify kubernetes object, annotations can be used by external tools which read, write and interact with it.

```sh
apiVersion: v1
kind: Pod
metadata:
  name: my-annotation-pod
  annotations:
    owner: mogueye87@gmail.com
    git-commit: bdab0c6
spec:
  containers:
  - name: nginx
    image: nginx
```