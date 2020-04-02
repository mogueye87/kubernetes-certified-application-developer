# Volumes 
Internal storage of a volume are ephemeral, Volume allow to provide more storage to a container.
```sh
apiVersion: v1
kind: Pod
metadata:
  name: volume-pod
spec:
  containers:
  - name: busybox
    image: busybox
    command: ['/bin/sh', '-c', "while true; sleep 3600; done;"]
    volumeMounts:
    - mountPath: /tmp/storage
      name: my-volume      
   volumes:
   - name: my-volume
     emptyDir: {}     
```