# Helm Chart for Tabby AI coding assistant

This chart allows you to deploy [Tabby](https://github.com/TabbyML/tabby) within Kubernetes.

## Installation

### Create a namespace
```shell
kubectl create ns tabby
```

### Installation

You should create your own `values.yaml` file to match your deployment preferences:

`values-custom.yaml`
```yaml
replicaCount: 1

ingress:
  enabled: true
  className: "nginx"
  annotations:
     cert-manager.io/cluster-issuer: "letsencrypt-prod"
  hosts:
    - host: domain.com
      paths:
        - path: /
          pathType: ImplementationSpecific
  tls:
    - secretName: tls-secret-tabby
      hosts:
        - domain.com

resources:
   limits:
     cpu: 4000m
     memory: 8192Mi
     nvidia.com/gpu: 1
   requests:
     cpu: 1000m
     memory: 4096Mi
     nvidia.com/gpu: 1

storage:
  className: "local-path"

env:
  DEVICE: cuda
  MODEL: TabbyML/DeepseekCoder-6.7B
```

```shell
helm upgrade --install -n tabby tabby-release -f values.yaml -f values-custom.yaml .
```



## Removal

```shell
helm uninstall -n tabby tabby-release
```