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
│   └── demo
└── infrastructure
    ├── configs
    └── controllers
        ├── opensearch
        └── prometheus
```

### Applications

The apps configuration is structured into:

- **apps/base/** dir contains namespaces and Helm release definitions
- **apps/production/** dir contains the production Helm release values
- **apps/demo/** dir contains the demo values

### Infrastructure

The infrastructure is structured into:

- **infrastructure/controllers/** dir contains namespaces and Helm release definitions for Kubernetes controllers
- **infrastructure/configs/** dir contains Kubernetes custom resources such as cert issuers and networks policies

### Clusters

The clusters is structured into:

- **clusters/production/** dir contains the Flux Kustomization definitions to bootstrap the cluster
- **clusters/demo/** dir contains the Flux Kustomization definitions to bootstrap the cluster

## Deployment

FluxCD is used to continuously deploy the application based on the configuration stored in this Git repository.
Install FluxCD into your Kubernetes cluster. This can be done using the instructions in the FluxCD documentation or use Terraform as shown in [ImperialOps/terraform-k8s-fluxcd](https://github.com/ImperialOps/terraform-aws-eks). NOTE TODO

## Credits

OG Boss [Stefan Prodan](https://github.com/stefanprodan) deserves all the credits with the [flux2-kustomize-helm-example](https://github.com/fluxcd/flux2-kustomize-helm-example) repository.
