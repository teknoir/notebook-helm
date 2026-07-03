# Notebook HelmChart

> **The orbital deployment engine.** The Notebook HelmChart turns a compact values file into a Kubernetes-hosted Jupyter Notebook runtime.

## Identity

| Field | Value |
| --- | --- |
| Catalog name | `notebook-helm` |
| Namespace | `teknoir` |
| Type | `helmchart` |
| Chart | `notebook` |
| Version | `0.0.2` |
| Registry | `teknoir.github.io/notebook-helm` |

## Deploy

```bash
helm repo add teknoir-notebook https://teknoir.github.io/notebook-helm/
helm install notebook teknoir-notebook/notebook -f values.yaml
```

## Teknoir platform manifest

```yaml
apiVersion: helm.cattle.io/v1
kind: HelmChart
metadata:
  name: notebook
  namespace: default
spec:
  repo: https://teknoir.github.io/notebook-helm
  chart: notebook
  targetNamespace: default
```

## Control panel

| Value | Default | Purpose |
| --- | --- | --- |
| `image.repository` | `jupyter/datascience-notebook` | Runtime image source. |
| `image.tag` | `latest` | Runtime image version. |
| `image.pullPolicy` | `Always` | Keeps the runtime fresh on deploy. |
| `resources.requests.memory` | `512Mi` | Baseline memory reservation. |
| `resources.limits.cpu` | `1500m` | CPU ceiling for the Notebook container. |
| `nodePort.enabled` | `false` | Switches the service from `ClusterIP` to `NodePort`. |

## Kubernetes footprint

- Creates one `Deployment` named `notebook`.
- Exposes HTTP traffic on service port `8888`.
- Uses `Recreate` rollout strategy for a single active workspace pod.
- Mounts host storage at `/home/jovyan` from `/opt/teknoir/notebook`.
