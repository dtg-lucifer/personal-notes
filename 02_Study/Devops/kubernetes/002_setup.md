# With minikube

> **What is minikube?**
> Minikube is a utility tool which allows us to learn kubernetes by deploying apps to our local machine and configuring a ***single node*** cluster inside our local machine to pracitce the kubernetes before going to any cloud hosted or any on premise kubernetes clusters.

#### *After installation steps*

After installing the minikube to start the single node cluster we need to run this command
```bash
minikube start
```

To get the details about urrently running nodes run this
```
kubectl get nodes
```

==To check one of the deployed pods are working or not we can deploy another pod with the busybox image and then accesing that busybix pod and from inside that we can try to ping the other pods with their ip addresses, if it succeeds then the pods are running properly==

***OR***

==We can check the logs for the pods we want to check the health of==

```bash
kubectl logs pod-name -n namespace-of-the-pod
```