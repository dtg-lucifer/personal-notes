
# To get the initial admin password 

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
```

# Open the argocd gui hosted on the kubernetes cluster

```bash
# To expose the ip
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'

# Port forward to the internal ip
kubectl port-forward svc/argocd-server -n argocd 8080:443
```