
# What are the components of kubernetes 

There multiple components which are coupled together to make kubernetes work properly, which are shown in the image below.

![[Pasted image 20240915221307.png]]

> *Each of the components serve various and unique purposes itself*

# Components
Kubernetes is a powerful system for managing containerized applications across multiple hosts. Here are its main components and their functions:

#### Control Plane
1. **API Server**: Acts as the front-end for the Kubernetes control plane. It exposes the Kubernetes API.
2. **etcd**: A consistent and highly-available key-value store used for all cluster data.
3. **Controller Manager**: Runs controller processes to regulate the state of the cluster.
4. **Scheduler**: Assigns workloads to specific nodes based on resource availability.

#### Nodes
1. **kubelet**: Ensures that containers are running in a Pod.
2. **kube-proxy**: Maintains network rules on nodes, allowing communication to your Pods.
3. **Container Runtime**: Software responsible for running containers (e.g., Docker, containerd).

#### Integration
- **Cloud Provider API**: Optional component for integrating with cloud services.

This architecture ensures efficient management and scaling of applications. Do you have any specific questions about these components?

# How do they work together
![[Pasted image 20240915230948.png]]