# What is Docker
Docker is an open-source platform that allows developers to build, deploy, and manage applications inside containers. [Containers are lightweight, standalone, and executable software packages that include everything needed to run a piece of software, including the code, runtime, system tools, libraries, and settings](https://www.howtogeek.com/devops/what-does-docker-do-and-when-should-you-use-it/)[1](https://www.howtogeek.com/devops/what-does-docker-do-and-when-should-you-use-it/)[2](https://www.howtogeek.com/733522/docker-for-beginners-everything-you-need-to-know/).

Here are some key points about Docker:

- **Isolation**: Containers provide an isolated environment for applications, ensuring that they run the same way regardless of where they are deployed.
- **Efficiency**: Unlike virtual machines, containers share the host system’s kernel, making them more lightweight and faster to start.
- **Portability**: Docker containers can run on any system that supports Docker, making it easy to move applications between different environments.
- [**Consistency**: By packaging all dependencies within the container, Docker ensures that applications run consistently across different environments, reducing the “it works on my machine” problem](https://www.howtogeek.com/733522/docker-for-beginners-everything-you-need-to-know/)

# Methodologies around Docker

1. **Containers**: Containers are lightweight, isolated environments that package an application along with all its dependencies (libraries, system tools, etc.). Unlike virtual machines (VMs), which run a full operating system, Docker containers share the host’s kernel and virtualize at a software level. This makes them faster to start and more efficient.
    
2. **Docker Images**: An image defines the software available in a container. Think of it as equivalent to starting a VM with an operating system ISO. You create an image by writing instructions in a **Dockerfile**, which Docker then uses to construct the image.
    
3. **Docker CLI and Daemon**: The Docker Command Line Interface (CLI) allows you to interact with Docker in your terminal. The CLI sends commands to a **Docker daemon**, which manages containers and the images they’re created from. The daemon can run locally or on a remote host.
    
4. **Container Runtimes**: The container runtime invokes kernel features to launch containers. Docker is compatible with runtimes adhering to the **OCI specification**, an open standard for containerization.
	
5. **Container registry:** A **Docker image registry** is a centralized location for storing and sharing container images. It can be either public or private. [Docker Hub, for instance, is a public registry that anyone can use and is the default choice](https://hub.docker.com/_/registry)[1](https://hub.docker.com/_/registry). [If you’re interested in creating your own private registry, you can set up a self-hosted one to manage repositories, push and pull images, and control repository access](https://hub.docker.com/_/registry)[2](https://www.baeldung.com/ops/docker-push-image-self-hosted-registry). Essentially, a registry allows you to manage and distribute container images efficiently. 🐳

6. **Cluster:** A cluster refers to a group of interconnected computing resources (such as servers, virtual machines, or cloud instances) that work together as a single unit. In the world of containers and orchestration, clusters play a crucial role in managing and deploying applications efficiently. Here are some key points:
	- Container Clusters:
	    - Definition: A container cluster consists of multiple nodes (machines) that collectively host and manage containers.
	    - Nodes:
	        - Worker Nodes: These nodes execute containerized applications. They run the actual containers.
	        - Control Plane Nodes (or Master Nodes): These nodes manage the cluster. They handle tasks like scheduling containers, maintaining desired state, and scaling.
	    - Communication: Nodes communicate with each other to distribute workloads and maintain consistency.
	    - Benefits:
	        - High Availability: Clusters ensure redundancy, so if one node fails, others can take over.
	        - Scalability: Easily add or remove nodes to handle varying workloads.
	        - Load Balancing: Distribute incoming requests across nodes.
	        - Resource Utilization: Efficiently allocate resources among containers.
	    - Examples:
	        - Kubernetes: Uses a cluster model with master and worker nodes.
	        - Docker Swarm: Also organizes containers into clusters for orchestration.
	- Orchestration:
	    - Purpose: Orchestration tools (like Kubernetes, Docker Swarm, or Amazon ECS) manage containerized applications within a cluster.
	    - Tasks:
	        - Scheduling: Deciding where to run containers based on resource availability and constraints.
	        - Scaling: Automatically adjusting the number of replicas based on demand.
	        - Health Monitoring: Ensuring containers are healthy and restarting failed ones.
	        - Networking: Managing communication between containers.
	        - Service Discovery: Allowing containers to find each other.
	    - Benefits: Orchestration simplifies deployment, scaling, and maintenance of containerized apps.
	- Use Cases:
	    - Microservices Architecture: Clusters are essential for deploying microservices-based applications.
	    - Cloud-Native Apps: Modern applications benefit from container clusters due to their flexibility and scalability.
	In summary, a cluster provides the foundation for orchestrating containers, enabling efficient resource utilization and streamlined management. 🌟🐳

7. **Cluster management:** 
	1. **Docker Swarm**:    
	    - **Definition**: Docker Swarm is an open-source platform for container orchestration. It allows you to manage and deploy applications using a containerization approach.
	    - **Key Features**:
	        - **Cluster Management**: You can create a cluster of nodes (computers) that operate as a single system. These nodes include Swarm manager nodes (to manage the cluster) and worker nodes (to execute tasks assigned by the manager).
	        - **Service Abstraction**: Docker Swarm introduces the concept of “services.” Services define network configurations, resource limits, and the number of container replicas.
	        - **Load Balancing**: Built-in load balancing ensures services interact without manual load balancer configuration.
	        - **Rolling Back**: Supports rolling back to previous service versions in case of deployment failures.
	        - **Scalability**: Easily adjust the number of container replicas.
	    - [**Use Case**: Docker Swarm is well-suited for smaller apps with fewer containers](https://phoenixnap.com/blog/kubernetes-vs-docker-swarm)[1](https://phoenixnap.com/blog/kubernetes-vs-docker-swarm).
	2. **Kubernetes (K8s)**:
	    - **Definition**: Kubernetes is a portable, open-source platform for managing containers and their workloads. It’s currently the most popular container orchestration tool.
	    - **Architecture**: A Kubernetes cluster consists of worker nodes managed by a Kubernetes master. Nodes can be virtual machines (VMs) or physical machines.
	    - **Advantages**:
	        - **Rich Functionality**: Offers service discovery, ingress, load balancing, self-healing, storage orchestration, scalability, and more.
	        - **Unified APIs**: Provides a unified set of APIs and strong guarantees about the cluster state.
	        - **Active Community**: Actively developed by a large community.
	        - **Wide Adoption**: Battle-tested by major players like Google and IBM.
	    - [**Ideal Use Case**: Complex applications that benefit from automatic scaling](https://www.howtogeek.com/devops/kubernetes-vs-docker-swarm-which-should-you-use/)[2](https://www.howtogeek.com/devops/kubernetes-vs-docker-swarm-which-should-you-use/).
	3. **Comparison**:
	    - Both tools have similar features but shine differently:
	        - **Docker Swarm**: Lightweight, easy to learn, and suitable for smaller apps.
	        - **Kubernetes**: More robust, complex, and ideal for large-scale production environments.
	    - [Consider your workload complexity, monitoring needs, security, and scalability when choosing between them](https://www.freecodecamp.org/news/kubernetes-vs-docker-swarm-what-is-the-difference/)[3](https://www.freecodecamp.org/news/kubernetes-vs-docker-swarm-what-is-the-difference/).
	
	In summary, Docker Swarm is simpler, while Kubernetes offers more advanced capabilities. Choose based on your specific requirements and expertise! 🐳🚀
 

## **Why Use Docker?**

- **Consistency**: Containers ensure that every environment (development, testing, production) is identical, reducing the “it works on my machine” problem.
- **Portability**: Develop once, run anywhere. Docker containers can be deployed on any system that supports Docker.
- **Efficiency**: Containers are lightweight and share the host’s kernel, making them faster and more resource-efficient than VMs. 

---

# How docker actually works
Docker consists of three basic columns

- **Docker client**
	- **Docker build**
	- **Docker pull**
	- **Docker run**
- **Docker host**
	- [[001_docker_networking]]
	- **Docker daemon**
		- **containers**
		- **images**
- **Registry**

### How the workflow of docker works?

1. First of all we have to follow the basic SDLC and build out needed apps and softwares so
2. After that we also need to build the `Dockerfile` which is actually the blueprint of our docker container
3. Therefore we have the build that image with the dockerfile 
4. Then we can push that image to an registry service to store that image so that we can pull that if we need that afterwards

### *Dockerfile rulesets* for writing the file with 

[Youtube video](https://youtu.be/1ymi24PeF3M?si=-OMvxAC5XCDq6yjF)

