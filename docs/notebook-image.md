# Notebook Image

> **The data science reactor core.** The Notebook Image component tracks the container runtime that supplies Jupyter, kernels, and the scientific Python universe.

## Identity

| Field | Value |
| --- | --- |
| Catalog name | `docker.io.jupyter.datascience-notebook` |
| Namespace | `teknoir` |
| Type | `image` |
| Repository | `docker.io/jupyter/datascience-notebook` |
| Version | `latest` |
| Lifecycle | `production` |

## Runtime payload

- Jupyter Notebook server for interactive computing.
- Data science libraries and kernels from the upstream Jupyter stack.
- A `jovyan` home workspace mounted by the Helm chart for persistence.

## Supply chain path

```mermaid
flowchart LR
    Upstream[Jupyter Image] --> Chart[Notebook HelmChart]
    Chart --> Pod[Notebook Pod]
    Pod --> Workspace[Persistent Workspace]
```

## Operational notes

- The chart defaults to `jupyter/datascience-notebook:latest` with `Always` pull policy.
- The container starts with `start-notebook.sh` and listens on port `8888`.
- File ownership is aligned to user and group `1000` before the Notebook container starts.

## Upgrade radar

- Pin a specific image tag when reproducibility matters.
- Validate notebook compatibility before changing the runtime image.
- Keep resource limits aligned with expected data workloads.
