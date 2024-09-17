
# What are manifests ?

Manifests are the various configuration files by which kubernetes can understand and build various objects which are needed. Such as *Deployments, services, Pods, ConfigMap, Secrets*. 

For more types of objects and policies refer to these:
- [[005_objects_classes]]
- [[007_policies]]

> Sometimes managing and writing these kinds of manifests can be tricky for a solo developer as to deploy planet scaled application needs at least more than 5 to 6 types of manifests depending on the workload. 
> 
> So kubectl provides us a way to generate the skeleton of various manifests so that we can therefore change some values as we need and start working right away

---

# How to generate ? 

Generating these manifests are as easy to run some commands with `kubectl`, actually we can simulate the workflow of manifests without actually creating them and running them and therefore capture the output as **YAML** and save to some files for furthur use.

> The `--dry-run` flag in `kubectl` is used to simulate the execution of a command without actually making any changes. This is particularly useful for testing and validating commands before applying them to your Kubernetes cluster. There are two main options for `--dry-run`:

1. **`--dry-run=client`**: This option simulates the command on the client side. It generates the output as if the command were executed, but it doesn’t send any request to the Kubernetes API server. This is useful for quickly checking the command’s output and structure.
    
    - Example: `kubectl create deployment nginx --image=nginx --dry-run=client -o yaml`
    - This command will output the YAML configuration for creating a deployment without actually creating it.
2. **`--dry-run=server`**: This option simulates the command on the server side. It sends the request to the Kubernetes API server, which validates and processes the request, but doesn’t persist the changes. This ensures that the command would succeed if it were actually executed.
    
    - Example: `kubectl create deployment nginx --image=nginx --dry-run=server -o yaml`
    - This command will send the request to the server, validate it, and return the YAML configuration, ensuring that the deployment can be created successfully.

[Using these options helps you verify your commands and configurations before applying them, reducing the risk of errors in your Kubernetes environment](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_run/)[1](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_run/)[2](https://www.goglides.dev/bkpandey/-dry-run-client-vs-server-vs-none-500f).

Do you have any specific scenarios in mind where you’d like to use these options?

---

# Generating a *Deployment* manifest

```bash
kubectl create deployment \
	--dry-run=client \
	--image nginx:alpine \
	reverse-proxy \
	-o yaml > deployment/file/path.yaml
```


# Generating a *Service* manifest (Nodeport)

```bash
kubectl create service nodeport my-service \
	--tcp="80:80" \
	--node-port=30001 \
	--dry-run=client \
	-o yaml > /services/file/path.yaml
```

# Generating an *Ingress* manifest
[What is an ingress?](005_objects_classes#Ingress)

```bash
kubectl create ingress ingress-name \
	--rule="deployment-label/=servicename:80" \
	--dry-run=client \ 
	-o yaml > /ingress/file/path.yaml
```

