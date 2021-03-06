Additional Information and Resources
Your supermarket company is in the process of moving their infrastructure to a Kubernetes platform in the cloud. This is sometimes challenging, because some of the older, legacy portions of that infrastructure have non-standard requirements. One of these legacy applications is a web service that provides a list of the various types of fruit the company sells in its stores.

This service has already been packaged into a container image, but there is one special requirement: The legacy app is hard-coded to only serve content on port 8775, but the team wants to be able to access the service using the standard port 80. Your task is to build a Kubernetes pod that runs this legacy container and uses the ambassador design pattern to expose access to the service on port 80.

This setup will need to meet the following specifications:

The pod should have the name fruit-service.
The fruit-service pod should have a container that runs the legacy fruit service image: linuxacademycontent/legacy-fruit-service:1.
The fruit-service pod should have an ambassador container that runs the haproxy:1.7 image and proxies incoming traffic on port 80 to the legacy service on port 8775 (the HAProxy configuration for this is provided below).
Port 80 should be exposed as a containerPort. Note that you do not need to expose port 8775.
The HAProxy configuration should be stored in a ConfigMap called fruit-service-ambassador-config.
The HAProxy config should be provided to the ambassador container using a volume mount that places the data from the ConfigMap in a file at /usr/local/etc/haproxy/haproxy.cfg.
haproxy.cfg should contain the following configuration data:


If everything is working correctly, you should be able to access fruit-service from another pod.

You can create a busybox pod to use for testing with a file called busybox.yml.

apiVersion: v1
kind: Pod
metadata:
  name: busybox
spec:
  containers:
  - name: myapp-container
    image: radial/busyboxplus:curl
    command: ['sh', '-c', 'while true; do sleep 3600; done']
Create the busybox testing pod.

kubectl apply -f busybox.yml
Use the busybox pod to test the legacy service on port 80. This command uses a subcommand to get the cluster's IP address for the pod and executes a curl command in the busybox pod to access the legacy service on port 80.

kubectl exec busybox -- curl $(kubectl get pod fruit-service -o=custom-columns=IP:.status.podIP --no-headers):80
If everything is working, you should see some JSON listing various types of fruit.
