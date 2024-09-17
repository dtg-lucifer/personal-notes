---
documentation: https://kubernetes.io/docs/home/
---

# What is kubernetes

Kubernetes is a container orchestration platform which is used in production grade software management. 
It single handedly manages scaling up and down clusters of nodes (application running in containers) whenever there is need to do so.

> What is k8s ?
> 	The 8 between the ***k*** and ***s*** stands for the other 8 letters in the kubernetes word which are `ubernete`
> Basically ***kubernetes*** stands for pilot or helmsman of a ship in the greek meaning.
> [Documentation](https://kubernetes.io/docs/home/)

Just like the captain of a ship make decision where to go same way kubernets also managees the deployed nodes and clusters

### Architecture of kubernetes
![[Pasted image 20240915221421.png]]

> ***Kubernetes components***
![[Pasted image 20240915221307.png]]

# Why is this so good ??

This allows companies t odeploy their applications into container and then when there are more requests kuberntes will automatically increase the number of pods and when there are no more requests it will automatically remove those extra containers. 

> It will provide the huge elasticity of deployments and request management and also it will save money in terms of compute resources

***The case study of spotify shows that after migrating from Helios to Kubernetes spotifiy now can handle 10 milllion requests per second easily***

# Some terms frequently used in kubernetes world

- **Cluster:** A set of machines (nodes) running Kubernetes. It’s the collective computing power that Kubernetes manages.
- **Node:** A single machine (either physical or virtual) in the Kubernetes cluster. There are two types:
    - **Master Node (Control Plane):** Manages the cluster, handles scheduling, and maintains the desired state of the cluster.
    - **Worker Node:** Runs the containerized applications (pods) that are managed by the master node.
- **Pod:** The smallest deployable unit in Kubernetes, a pod can contain one or more containers that share storage, network, and a specification on how to run.
- **Service:** An abstraction that defines a logical set of pods and a policy to access them. Services provide stable IP addresses and DNS names for the pods.
- **Namespace:** A way to divide cluster resources between multiple users or teams. It helps in organizing objects in the cluster and controlling access.
- **Deployment:** A controller that provides declarative updates to applications, ensuring that a specified number of replicas of a pod are running at any time.
- **ReplicaSet:** Ensures that a specified number of pod replicas are running at any given time. It’s usually managed by a deployment.
- **ConfigMap and Secret:** ConfigMap is used to store non-confidential configuration data in key-value pairs, while Secret is used for storing sensitive data like passwords and tokens.
- **Ingress:** Manages external access to the services in a cluster, typically HTTP or HTTPS routes.

# Advanced Kubernetes Concepts:

- **StatefulSet:** Manages stateful applications, providing unique identities to each pod, often used with databases.
- **DaemonSet:** Ensures that a copy of a pod runs on all (or some) nodes in the cluster. Useful for logging or monitoring agents.
- **Helm:** A package manager for Kubernetes, Helm helps in managing Kubernetes applications by defining, installing, and upgrading even the most complex Kubernetes applications.
- **Persistent Volume (PV) and Persistent Volume Claim (PVC):** PV is a piece of storage in the cluster that has been provisioned by an administrator, while PVC is a request for storage by a user.
- **Kubelet:** An agent that runs on each node in the cluster and ensures that the containers are running in a pod.
- **Kube-proxy:** Maintains network rules on nodes and allows network communication to your pods from inside or outside the cluster.


# Hands-On Practice:

- **Minikube:** A tool that runs a single-node Kubernetes cluster on your local machine for learning and testing.
- **Kind (Kubernetes in Docker):** A tool for running local Kubernetes clusters using Docker container nodes.
- **K3s:** A lightweight Kubernetes distribution for IoT and edge computing, perfect for running Kubernetes on resource-constrained environments.