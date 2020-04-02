# Services
> A service is an abstraction layer that allows an access to a set of pods in kubernetes cluster.
```sh
apiVersion: v1
kind: Service
metadata: 
  name: nginx-svc
  labels:
    app: nginx-svc
spec:
    # define the type of service
    type: ClusterIP    
    selector:
      app: nginx-server
    ports:
    - protocol: TCP
      port: 8080  # define the ports of the service we listen on
      targetPort: 80 # defines the port on which we want redirect traffic.        
```