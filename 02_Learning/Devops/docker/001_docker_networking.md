---
tags:
  - docker
  - devops
  - networking
---
# What is docker networks?

Docker networking enables communication between containers, external services, and your Docker host. Here are the key network types and examples for each:

- **Default Bridge Network**
    - Automatically created when Docker is installed
    - Acts like a switch, connecting containers
    - Requires manual port exposure for external access
    
- **User-Defined Bridge Network**
    - Custom networks created by users
    - Provides isolation between containers
    - Supports container-to-container DNS resolution
    
- **Host Network** 
    - Containers share the host’s network stack
    - No network isolation
    - Useful for performance-sensitive applications

- **Macvlan Network**    
    - Containers get their own MAC addresses
    - Directly connect to the physical network
    - Acts like virtual machines on the network

- **IPVlan Network**    
    - Containers connect to the host like a router
    - No broadcast traffic
    - Ideal for complex network setups

- **Overlay Network** 
    - Connects containers across multiple hosts
    - Used in Docker Swarm or Kubernetes
    - Simplifies multi-host networking

- **None Network**
    - Completely isolates the container
    - No network connectivity
    - Useful for security-sensitive applications

These networks provide flexibility and control over how containers communicate and interact with each other and external systems.

