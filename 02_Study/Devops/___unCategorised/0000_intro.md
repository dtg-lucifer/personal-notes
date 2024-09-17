---
tags:
  - devops
  - intro
---
# Table of contents

1. [[#What is DevOps? Why DevOps?]]
2. [[#Phases of DevOps]]
3. [[#Three Columns of DevOps]]
4. [[#Roadmap to learn DevOps]]
5. [[#10 Best DevOps Tools]]

---
# What is DevOps? Why DevOps?

Basically in the big tech companies when the tech team size increases by a lot therefore a topic comes to manage the whole process of development and deployment, which is **Devops**

**DevOps** is a set of practices and a framework that brings together IT teams to enhance software development outcomes. [The goal is to create a collaborative experience by leveraging different skill sets across multiple disciplines, ultimately improving the quality of the finished product](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-devops/)[1](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-devops/). In essence, DevOps unifies people, processes, and technology to continually provide value to customers. Here’s how it works:

1. **Development (Dev)**: This phase involves coding, testing, reviewing, and integrating code. DevOps teams innovate rapidly while maintaining quality and stability through automation and continuous integration.
2. **Operations (Ops)**: The Ops phase focuses on deploying applications into production environments consistently and reliably. It also includes configuring the foundational infrastructure.
3. **Collaboration**: DevOps encourages formerly siloed roles (development, IT operations, quality engineering, and security) to coordinate and collaborate. By adopting a DevOps culture, teams respond better to customer needs and achieve business goals faster.

[In summary, DevOps accelerates software delivery, making it more efficient, reliable, and responsive to market demands](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-devops/)[1](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-devops/)[2](https://www.ibm.com/topics/devops). 🚀

![[Pasted image 20240722233100.png]]

# Phases of DevOps

The whole concept of **devops** follows some steps defined in the picture.

```bash
├── Plan
├── CI (Continuous integration)
│ └── Build
│ └── Test
├── CD (Continuous Development)
│ └── Release
│ └── Deploy
├── Operate
├── Monitor
├── Again Plan

So basically it forms an Infinity loop that is why the logo for the DevOps looks like Infinity
```

---
# Three Columns of DevOps

1. ***[[#infrastructure]]***
2. ***[[#automation]]***
3. ***[[#monitoring]]***

### infrastructure
If we need to deliver a software then we would probably need a server to deploy the software and also a database to store the data and other things which rely on some kind of hardware. ***These are called the infrastructure***
### automation
This is to automate the process of making or creating the infrastructure or anything similar to that using the technologies such as **Terraform**.
### monitoring
Keeping track about how our app is working and finding any issues that the app is facing or is it slower than before and all.

---

# Roadmap to learn DevOps

Free online books - [ahmedamsaleh/Free-DevOps-Books-1: A curated collection of free DevOps related eBooks (github.com)](https://github.com/ahmedamsaleh/Free-DevOps-Books-1/)
```
version control
linux
coding
agile development
operations
docker/kubernetes
ansible
jenkins
monitoring
```

1. ***[[#linux]]**
2. ***[[#networking]]***
3. ***[[#virtualisation]]*** 
4. Programming and Git
5. Cloud Providers (AWS, 30 - 40 services and how they work)
6. ***[[#IAC]]*** (Infrastucture as Code)
7. ***[[#CI/CD]]***
8. ***[[#Containerization]]***
### Linux
- File systems
- Text editors
- Shell scripting
- SSH
- Virualisation
- Package management
- Process and service management
- Practice - How to make a web server, how to setup a database, user and group management, install different different devops tools9 docker, jenkins, terraform)

### Scripting
- Learn any of these languages - Python, bash, go
- Scripting is used for these 
	- Backup automation
	- working with API
	- integration with other devops tools
	- system cleanip automation
	- email notification script
	- software update automation
	- log analysis automatin
	- network diagnosis scriopt 
	- data tranformation automation
	- user account management script

### Advanced GIT
- rebase
- cherry pick
- and many other complex workflows

### Networking
Important topics - IP Addressing, ip protocols TCP/IP, UDP, HTTP, DNS, networking services - DHCP, DNS, routing and switching basics, authentication and atuthorizations, security best practicesm shift left security, firewalls and networkd security

Full video - https://youtu.be/qiQR5rTSshw?si=ZmYE3Cr5lKQYFhPr
- DNS
- Private subnet
- Advanced topics
- TCP/IP Protocols and ports
- Routing and gateways (NAT)
- CIDR/Subnetting
- Security - DevSecOps
### Virtualisation
- What is virtualisation
- operating systems

### IAC
it stands for **Infrastrucutre as code**. this states the provisioning and managing the infrastrucutre using code.
Prerequisites: ***YAML, JSON***

- How **terraform** works
- Provisioners and providers and resources in **Terraform**
- What is ansible and learn more about that
- ANSIBLE

### CI/CD
- learn pipelines 
- gitlabs, jenkins, circle ci

### Containerization
- Docker
- Kubernetes
---

# 10 Best DevOps Tools

### 1. [Jenkins](https://www.geeksforgeeks.org/what-is-jenkins)

- ****Purpose:**** Continuous Integration and Continuous Delivery (CI/CD)
- ****Features:**** Extensive plugin ecosystem, automation of build and deployment processes, and scalability.

### 2. [Docker](https://www.geeksforgeeks.org/introduction-to-docker)

- ****Purpose:**** Containerization
- ****Features:**** Simplifies application deployment, ensures consistency across environments, and supports microservices architecture.

### 3. [Kubernetes](https://www.geeksforgeeks.org/introduction-to-kubernetes-k8s)

- ****Purpose:**** Container Orchestration
- ****Features:**** Automates deployment, scaling, and management of containerized applications.

### 4. [Terraform](https://www.geeksforgeeks.org/what-is-terraform)

- ****Purpose:**** Infrastructure as Code (IaC)
- ****Features:**** Manages infrastructure across multiple cloud providers, ensures reproducibility, and supports version control.

### 5. [Ansible](https://www.geeksforgeeks.org/ansible)

- ****Purpose:**** Configuration Management and Automation
- ****Features:**** Simple syntax (YAML), agentless architecture, and scalability.

### 6. [Prometheus](https://www.geeksforgeeks.org/kubernetes-prometheus)

- ****Purpose:**** Monitoring and Alerting
- ****Features:**** Collects and stores metrics, powerful querying language (PromQL), and integration with Grafana for visualization.

### 7. [GitLab](https://www.geeksforgeeks.org/gitlab)

- ****Purpose:**** Source Code Management and CI/CD
- ****Features:**** Integrated DevOps platform, supports code versioning, CI/CD pipelines, and project management tools.

### 8. [ELK Stack (Elasticsearch, Logstash, Kibana)](https://www.geeksforgeeks.org/what-is-elastic-stack-and-elasticsearch)

- ****Purpose:**** Logging and Analytics
- ****Features:**** Real-time data search and analysis, log aggregation, and powerful visualization capabilities.

### 9. [Azure DevOps](https://www.geeksforgeeks.org/azure-devops-an-introduction)

- ****Purpose:**** End-to-End DevOps Solution
- ****Features:**** Supports CI/CD, project management, and integrates with various development and monitoring tools.

### 10. [Nagios](https://www.geeksforgeeks.org/how-to-install-nagios-on-ubuntu)

- ****Purpose:**** Infrastructure Monitoring
- ****Features:**** Monitors network services, server resources, and provides alerts for potential issues.
---
![[Pasted image 20240727230424.png]]