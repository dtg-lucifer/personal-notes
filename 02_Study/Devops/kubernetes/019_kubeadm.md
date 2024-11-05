**Kubeadm** is a tool designed to simplify the process of setting up a Kubernetes cluster. It provides `kubeadm init` and `kubeadm join` as best-practice “fast paths” for creating Kubernetes clusters. [Kubeadm handles the necessary steps to get a minimum viable cluster up and running, focusing on bootstrapping rather than provisioning machines](https://kubernetes.io/docs/reference/setup-tools/kubeadm/)[1](https://kubernetes.io/docs/reference/setup-tools/kubeadm/).

### Steps to Configure and Provision a Kubernetes Cluster with Kubeadm

#### Prerequisites

1. **Linux Hosts**: Ensure you have one or more machines running a deb/rpm-compatible Linux OS (e.g., Ubuntu or CentOS).
2. **Resources**: Each machine should have at least 2 GB of RAM and 2 CPUs.
3. **Network Connectivity**: Full network connectivity between all machines in the cluster.
4. **Unique Hostnames**: Each node should have a unique hostname, MAC address, and product_uuid.
5. **Open Ports**: Ensure required ports are open on your machines.

#### Step-by-Step Guide

1. **Install Docker** (or another container runtime) on all nodes:
    
    ```bash
    sudo apt-get update
    sudo apt-get install -y docker.io
    sudo systemctl enable docker
    sudo systemctl start docker
    ```
    
2. **Install Kubeadm, Kubelet, and Kubectl** on all nodes:
    
    ```bash
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl
    sudo curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
    sudo apt-get update
    sudo apt-get install -y kubelet kubeadm kubectl
    sudo apt-mark hold kubelet kubeadm kubectl
    ```
    
3. **Disable Swap** on all nodes:
    
    ```bash
    sudo swapoff -a
    sudo sed -i '/ swap / s/^/#/' /etc/fstab
    ```
    
4. **Initialize the Control Plane** on the master node:
    
    ```bash
    sudo kubeadm init --pod-network-cidr=192.168.0.0/16
    ```
    
5. **Set Up Local kubeconfig** on the master node:
    
    ```bash
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```
    
6. **Install a Pod Network Add-on** (e.g., Calico):
    
    ```bash
    kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
    ```
    
7. **Join Worker Nodes** to the cluster: On each worker node, run the command provided by `kubeadm init` on the master node. It will look something like this:
    
    ```bash
    sudo kubeadm join <master-node-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
    ```
    

### Additional Resources

[For more detailed instructions and advanced configurations, you can refer to the](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/) [2](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/).
