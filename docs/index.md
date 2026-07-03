# Teknoir Notebook TechDocs

> **Launchpad for data science at the edge.** A compact constellation of Backstage components that turns a Helm release into a ready-to-use Jupyter data science cockpit.

## Component constellation

| Component | Type | Mission |
| --- | --- | --- |
| [Notebook App](notebook-app.md) | `app` | The user-facing Jupyter Notebook experience for data science workflows. |
| [Notebook HelmChart](notebook-helm.md) | `helmchart` | The Kubernetes delivery engine for deploying Notebook into Teknoir environments. |
| [Notebook Image](notebook-image.md) | `image` | The Jupyter Data Science Stack runtime that powers notebooks, kernels, and libraries. |

## Signal flow

```mermaid
flowchart LR
    Image[Notebook Image] --> Helm[Notebook HelmChart]
    Helm --> App[Notebook App]
    App --> User[Data Scientist]
```

## Quick coordinates

- **Owner:** `group:teknoir/public`
- **System:** `system:teknoir/core`
- **Lifecycle:** `production`
- **Repository:** `teknoir/notebook-helm`
- **Helm registry:** `https://teknoir.github.io/notebook-helm`

## Operator pulse

- Port `8888` exposes the Notebook interface.
- Persistent workspace data lands in `/opt/teknoir/notebook` on the host.
- Default runtime image is `jupyter/datascience-notebook:latest`.
- Chart version `0.0.2` is the current release advertised in the catalog.
