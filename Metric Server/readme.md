> Kubernetes metrics server  provides an API which allow access data about nodes and pods such memory,
> CPU usage.

```sh
$ cd ~/
$ git clone https://github.com/linuxacademy/metrics-server
$ kubectl apply -f ~/metrics-server/deploy/1.8+/
```

Once you have installed the metrics server, you can use this command to verify that it is responsive:

`kubectl get --raw /apis/metrics.k8s.io/`