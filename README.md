# Kubernetes GitOps :slightly_smiling_face:

[![validate](https://github.com/ImperialOps/gitops/workflows/validate/badge.svg)](https://github.com/ImperialOps/gitops/actions)

This repository contains the Kubernetes manifests for applications deployed using GitOps principles with FluxCD. It uses Kustomize and Helm to minimize duplication.

## Repository Structure

The repository is structured as follows:

```text
├── apps
│   ├── base
│   │   └── airgap-webhook
│   ├── demo
│   └── production
├── clusters
│   ├── dev
│   └── kind
│       └── flux-system
└── infrastructure
    ├── base
    ├── dev
    │   ├── configs
    │   └── controllers
    └── kind
```

### Applications

The apps configuration is structured into:

- **apps/base/** dir contains namespaces and Helm release definitions
- **apps/kind/** dir contains the dev values for local development & testing
- **apps/dev/** dir contains the dev values for larger clusters

### Infrastructure

The infrastructure is structured into:

- **infrastructure/base/** dir contains namespaces and Helm release definitions for all clusters
- **infrastructure/kind/** dir contains Kubernetes custom resources such as nginx ingress
- **infrastructure/dev/** dir contains Kubernetes custom resources such as cert issuers and service mesh

### Clusters

The clusters is structured into:

- **clusters/dev/** dir contains the Flux Kustomization definitions to bootstrap the cluster
- **clusters/kind/** dir contains the Flux Kustomization definitions to bootstrap the cluster

## Deployment

```bash
# kind cluster with host ports
# config source: https://kind.sigs.k8s.io/docs/user/ingress/
kind create cluster --name flux --config kind.yaml

# fork repo and export creds
export GITHUB_TOKEN=<your-token>
export GITHUB_USER=<your-username>

# bootstrap cluster
flux bootstrap github --owner=$GITHUB_USER --repository=<your-repo> --branch=main --path=./clusters/kind --personal

# watch sync
flux get kustomizations --watch
```

## Credits

OG Boss [Stefan Prodan](https://github.com/stefanprodan) deserves all the credits with the [flux2-kustomize-helm-example](https://github.com/fluxcd/flux2-kustomize-helm-example) repository.
