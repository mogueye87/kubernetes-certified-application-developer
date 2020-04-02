# Multi-containers pod
## What is a multi-container pod
A multi-container pod is a pod that has more than one container, working together forming single unit, sharing resources and network
The containers in a pod communicates in  different ways:
* Shared Network
* Shared Storage volume
* Shared namespace process

## Multi-containers pod  design patterns
- **Sidecar pod**: add functionalities to an existing the main container, 
- **Ambassador pod**: Handle incoming traffic and redirect the traffic to the main container 
- ****: 