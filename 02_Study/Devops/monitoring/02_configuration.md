### Ways to configure prmetheus
> There are mainly two ways to configure prometheus
> One is through the command line and another is with the configuration file

### Some common configuration parametes
> ***Global configuration*** - control the behavious of prometheus globally
> ***Scrape intervals*** - change the frequency of metric collection
> ***Alerting rules*** - define conditions that trigger alerts
> ***Alertmanager configuration*** - control routing for alerts
> ***Service discovery*** - automatcially detect and monitor new targets
> ***Relabel config*** - dynamically adjust or modify labels

### Example ocnfiguration file

```yml
global:
  scrape_interval: 15s  # How often to scrape targets by default.
  evaluation_interval: 15s  # How often to evaluate rules by default.

  # Attach these labels to any time series or alerts when communicating with
  # external systems (federation, remote storage, Alertmanager).
  external_labels:
    monitor: 'codelab-monitor'

scrape_configs:
  # Scrape Prometheus itself
  - job_name: 'prometheus'
    scrape_interval: 5s  # Override the global default and scrape targets from this job every 5 seconds.
    static_configs:
      - targets: ['localhost:9090']

```

### Example configuration file to monitor kubernetes cluster
```yml
global:
  scrape_interval: 15s  # Default scrape interval

scrape_configs:
  - job_name: 'kubernetes-apiservers'
    kubernetes_sd_configs:
      - role: endpoints
    relabel_configs:
      - source_labels: [__meta_kubernetes_namespace]
        action: keep
        regex: default

  - job_name: 'kubernetes-nodes'
    kubernetes_sd_configs:
      - role: node
    relabel_configs:
      - source_labels: [__meta_kubernetes_node_label_role]
        action: keep
        regex: master

  - job_name: 'kubernetes-pods'
    kubernetes_sd_configs:
      - role: pod
    relabel_configs:
      - source_labels: [__meta_kubernetes_pod_label_app]
        action: keep
        regex: .*

  - job_name: 'kubernetes-services'
    kubernetes_sd_configs:
      - role: service
    relabel_configs:
      - source_labels: [__meta_kubernetes_service_label_app]
        action: keep
        regex: .*

```