# Notebook Helm Chart

This chart deploys Notebook to a Kubernetes cluster.

> The implementation of the Helm chart is right now the bare minimum to get it to work.

## Usage in Teknoir platform
Use the HelmChart to deploy the Notebook to a Device.

```yaml
---
apiVersion: helm.cattle.io/v1
kind: HelmChart
metadata:
  name: notebook
  namespace: default
spec:
  repo: https://teknoir.github.io/notebook-helm
  chart: notebook
  targetNamespace: default
  valuesContent: |-
    # Example for minimal configuration
    
```

## Adding the repository

```bash
helm repo add teknoir-notebook https://teknoir.github.io/notebook-helm/
```

## Installing the chart

```bash
helm install notebook teknoir-notebook/notebook -f values.yaml
```