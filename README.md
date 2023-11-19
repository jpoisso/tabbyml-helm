# Helm Chart for Tabby AI coding assistant

This chart allows you to deploy [Tabby](https://github.com/TabbyML/tabby) within Kubernetes.

## Installation

### Create a namespace
```shell
kubectl create ns tabby
```

### Installation

You should create your own `values.yaml` file to match your deployment preferences (see [values-example.yaml](tabbyml/values-example.yaml))


```shell
helm upgrade --install -n tabby tabby-release -f values.yaml -f values-example.yaml .
```



## Removal

```shell
helm uninstall -n tabby tabby-release
```