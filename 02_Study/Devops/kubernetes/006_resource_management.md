
# What is resource management for pods and services in kubernets !

**Resource management** in Kubernetes refers to controlling how much CPU, memory, and other resources a pod and its containers are allowed to use. This ensures that applications running in the cluster receive the necessary resources to operate efficiently, while also preventing resource starvation and overconsumption by any single pod or service. Resource management is crucial for maintaining the stability and performance of applications, especially in production environments where many workloads compete for finite resources.

### Key Concepts in Resource Management:

#### 1. **Resource Requests and Limits:**
   Kubernetes allows you to define the amount of **CPU** and **memory (RAM)** that each container in a pod can request and the maximum amount it is allowed to use.

   - **Requests:** The amount of CPU or memory that a container is guaranteed to have. The scheduler uses this value to determine on which node to place the pod, ensuring that the node has at least the requested resources available.
   - **Limits:** The maximum amount of CPU or memory a container is allowed to use. If the container exceeds this limit, it may be throttled (in the case of CPU) or terminated (in the case of memory).

   Defining requests and limits helps ensure resource efficiency and prevents pods from overloading nodes.

   **Example of Resource Requests and Limits in YAML:**
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: my-pod
   spec:
     containers:
     - name: my-container
       image: nginx
       resources:
         requests:
           memory: "128Mi"  # Memory request
           cpu: "500m"      # CPU request
         limits:
           memory: "256Mi"  # Memory limit
           cpu: "1"         # CPU limit
   ```

   - **CPU units:** CPU is measured in CPU units. `1` represents one full CPU core, and `500m` represents half of a CPU core.
   - **Memory units:** Memory is measured in bytes, with `Mi` representing Mebibytes (1 MiB = 1024^2 bytes) and `Gi` representing Gibibytes (1 GiB = 1024^3 bytes).

#### 2. **Quality of Service (QoS) Classes:**
   Kubernetes uses **QoS classes** to categorize pods based on their resource requests and limits. This ensures that critical workloads get prioritized access to resources, especially during times of resource contention.

   - **Guaranteed:** Pods where all containers have both memory and CPU requests and limits set to the same values. These pods have the highest priority and are less likely to be evicted when the node runs out of resources.
   - **Burstable:** Pods where containers have memory and/or CPU requests set, but limits may exceed the requests. These pods can use more resources if available but may be throttled or evicted if the system runs low on resources.
   - **BestEffort:** Pods where containers do not have any resource requests or limits defined. These pods have the lowest priority and are the first to be evicted in case of resource shortages.

#### 3. **Horizontal Pod Autoscaling (HPA):**
   **Horizontal Pod Autoscaling (HPA)** is a Kubernetes feature that automatically adjusts the number of pod replicas based on observed CPU utilization (or other custom metrics). It ensures that the application scales up or down to meet demand, thereby optimizing resource usage.

   - **Example:**
     ```yaml
     apiVersion: autoscaling/v2
     kind: HorizontalPodAutoscaler
     metadata:
       name: my-hpa
     spec:
       scaleTargetRef:
         apiVersion: apps/v1
         kind: Deployment
         name: my-deployment
       minReplicas: 2
       maxReplicas: 10
       metrics:
       - type: Resource
         resource:
           name: cpu
           target:
             type: Utilization
             averageUtilization: 50  # Target 50% CPU utilization
     ```

#### 4. **Vertical Pod Autoscaling (VPA):**
   **Vertical Pod Autoscaling (VPA)** automatically adjusts the resource requests and limits of containers within a pod based on their actual resource usage. If a container is using more CPU or memory than requested, VPA increases its resource requests. This is useful when workloads have variable resource needs over time.

   **Note:** VPA restarts the pods to apply the new resource requests.

#### 5. **LimitRanges:**
   A **LimitRange** is a Kubernetes object that sets default resource requests and limits for all pods and containers in a specific namespace. It helps to ensure that all workloads in a namespace adhere to defined resource usage constraints.

   **Example:**
   ```yaml
   apiVersion: v1
   kind: LimitRange
   metadata:
     name: cpu-mem-limit-range
     namespace: my-namespace
   spec:
     limits:
     - max:
         cpu: "2"
         memory: "1Gi"
       min:
         cpu: "200m"
         memory: "100Mi"
       type: Container
   ```

#### 6. **ResourceQuotas:**
   A **ResourceQuota** is a policy that defines the maximum amount of resources (CPU, memory, storage, etc.) that can be consumed by all the pods, services, or other Kubernetes objects in a namespace. This prevents a single namespace from consuming too many resources and ensures fair resource allocation across namespaces.

   **Example:**
   ```yaml
   apiVersion: v1
   kind: ResourceQuota
   metadata:
     name: compute-resources
     namespace: my-namespace
   spec:
     hard:
       requests.cpu: "10"       # Total CPU requests limit for the namespace
       requests.memory: "32Gi"  # Total memory requests limit
       limits.cpu: "20"         # Maximum CPU limit for the namespace
       limits.memory: "64Gi"    # Maximum memory limit
   ```

### Resource Management for Services:
Services in Kubernetes do not have direct resource constraints like CPU or memory. However, the management of services is closely related to the pods they expose. Here's how resource management interacts with services:

- **Scaling Pods via HPA:** When a service routes traffic to a deployment that is horizontally auto-scaled (via HPA), it automatically balances traffic across the scaled pods. Efficient pod resource management ensures that services can handle high loads without overloading any single pod.
- **Load Balancing:** Kubernetes services, especially **LoadBalancer** and **ClusterIP** types, distribute traffic based on pod availability and resource capacity. As the number of replicas scales (due to HPA or manual scaling), the service dynamically adjusts its routing.

### Summary of Resource Management:
- **Requests and Limits** ensure efficient resource utilization and prevent resource overconsumption.
- **QoS Classes** prioritize pods based on their resource requests, ensuring critical workloads have higher availability.
- **Horizontal and Vertical Autoscaling** dynamically adjusts the number of pods or their resource allocations based on current demand and resource usage.
- **LimitRanges and ResourceQuotas** provide global resource constraints within namespaces to enforce limits on resource consumption across the cluster.

By combining these features, Kubernetes ensures that applications are resilient, scalable, and operate efficiently while maximizing the usage of available resources.

### Example setup resource limits
```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pod-info-deployment
  namespace: development
  labels:
    app: pod-info
spec:
  replicas: 1
  selector:
    matchLabels:
      app: pod-info
  template:
    metadata:
      labels:
        app: pod-info
    spec:
      containers:
      - name: pod-info-container
        image: kimschles/pod-info-app:latest
        resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 3000
        env:
          - name: POD_NAME
            valueFrom:
              fieldRef:
                fieldPath: metadata.name
          - name: POD_NAMESPACE
            valueFrom:
              fieldRef:
                fieldPath: metadata.namespace
          - name: POD_IP
            valueFrom:
              fieldRef:
                fieldPath: status.podIP
```