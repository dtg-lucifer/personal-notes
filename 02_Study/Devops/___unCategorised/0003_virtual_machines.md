---
tags:
  - devops
  - vm
  - virtual-machines
---
# What is a Virtual Machine ?
- A virtual machine is a software-based emulation of a physical computer. It allows you to run multiple operating systems (OS) simultaneously on a single physical machine.
- Each VM behaves like an independent computer, complete with its own OS, applications, and resources.
- VMs are created using virtualization software and are stored as files on the host system.

# What is a Hypervisor ?
- A hypervisor (also known as a Virtual Machine Monitor or VMM) is the key component that enables virtualization.
- It sits between the physical hardware (host) and the VMs (guests).
- The hypervisor allocates and manages resources (CPU, memory, storage, etc.) for each VM.
- There are two main types of hypervisors:
    - **Type 1 (Bare Metal)**: Installs directly on the physical hardware. Examples include VMware ESXi, Xen, and Microsoft Hyper-V.
    - **Type 2 (Hosted)**: Runs on top of an existing operating system. Examples include VMware Workstation, Oracle VirtualBox, and Microsoft VirtualPC.

# How all of these works under the hood ?
- When you start a VM, the hypervisor intercepts its requests to the hardware.
- It allocates CPU time, memory, and other resources to each VM.
- The VMs run independently, unaware of each other, and share the host’s resources.
- This separation ensures security, portability, and efficient resource utilization.
---

# Type 1 Hypervisor

1. **Main Use of Type 1 Hypervisor**:
    - **Server Virtualization**: Type 1 hypervisors are primarily used for server virtualization. They allow you to consolidate multiple virtual machines (VMs) on a single physical server.
    - **Resource Isolation**: Type 1 hypervisors ensure strong isolation between VMs. Each VM runs its own OS and applications, preventing interference between workloads.
    - **Efficient Resource Utilization**: By sharing physical resources (CPU, memory, storage) among VMs, you maximize hardware utilization.
    - **High Availability**: Type 1 hypervisors support features like live migration, failover, and load balancing, ensuring uninterrupted service.
  
1. **Leveraging Type 1 Hypervisors in DevOps**:
    - **Development and Testing Environments**: DevOps teams can create isolated VMs for development, testing, and staging. This accelerates software development cycles.
    - **Infrastructure as Code (IaC)**: Type 1 hypervisors enable IaC tools (e.g., Terraform, Ansible) to provision and manage VMs programmatically.
    - **Continuous Integration/Continuous Deployment (CI/CD)**: VMs can be spun up dynamically for CI/CD pipelines, ensuring consistent environments.
    - **Scaling and Elasticity**: DevOps can scale VMs horizontally or vertically based on demand, using automation and orchestration tools.
    - **Disaster Recovery**: VM snapshots and replication help in disaster recovery planning.