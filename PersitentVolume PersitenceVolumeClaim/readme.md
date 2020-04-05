# Persistence Volume
> A Persistence Volume is a Kubernetes Object used for adding persitent storage to pod using nodes resources.


```sh
apiVersion: v1
# Persistence Volume Resource
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  storageClassName: local-storage
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 1Gi
  hostPath: 
    path: "/mnt/data"  
```

# PersistenceVolumeClaim
A PVC is a Kubernetes object that will claim the storage define in a PV using the storageClassName and accessModes.

```sh
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  storageClassName: local-storage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 512Mi
```

#Create a pod to consume storage resources using a PVC:
```sh
kind: Pod
apiVersion: v1
metadata:
  name: my-pvc-pod
spec:
  containers:
  - name: busybox
    image: busybox
    command: ["/bin/sh", "-c", "while true; do sleep 3600; done"]
    volumeMounts:
    - mountPath: "/mnt/storage"
      name: my-storage
  volumes:
  - name: my-storage
    persistentVolumeClaim:
      claimName: my-pvc
```

