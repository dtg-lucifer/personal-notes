
# What is HELM

**Helm** is a **package manager for Kubernetes** that simplifies the deployment and management of applications on Kubernetes clusters. Here are some key points about Helm:
- **Charts**: Helm uses packages called “charts” to define, install, and upgrade applications. A chart is a collection of files that describe a related set of Kubernetes resources.
- **Templating**: Helm charts use templates to allow for dynamic configuration. This means you can customize your deployments easily by changing values in a values file.
- **Release Management**: Helm tracks the versions of your applications and allows you to roll back to previous versions if needed.
- **Repository**: Helm charts can be stored in repositories, making it easy to share and reuse them.

---

# Example *Chart.yaml* file

```yaml
apiVersion:
name:
version:
kubeVersion:
description:
type:
keywords:
  - 
home:
sources:
  - 
dependencies:
  - name:
    version:
    repository:
    condition:
    tags:
      - 
    import-values:
      - 
    alias:
maintainers:
  - name:
    email:
    url:
icon:
appVersion:
deprecated:
annotations:
  example:

```
