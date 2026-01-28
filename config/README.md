<!--
# Copyright 2021 - 2025 Crunchy Data Solutions, Inc.
#
# SPDX-License-Identifier: Apache-2.0
-->


## Targets

- The `default` target installs the operator in the `postgres-operator`
  namespace and configures it to manage resources in all namespaces.

<!--
- The `dev` target installs the CRD and RBAC in the `postgres-operator`
  namespace while scaling an existing operator Deployment to zero.
-->


## Bases

- The `crd` base creates `CustomResourceDefinition`s that are managed by the
  operator.

- The `manager` base creates the `Deployment` that runs the operator. Do not
  run this as a target.

- The `rbac` base creates a `ClusterRole` that allows the operator to
  manage resources in all current and future namespaces.

## Single Install File

Render the kustomize single file, for easy installation:

> kustomize build config/default -o config/multi-ns-install.yaml

This can then be installed via either of:

> kubectl apply --server-side -f config/multi-ns-install.yaml

> kubectl apply --server-side -f https://raw.githubusercontent.com/iter8-au/postgres-operator/refs/heads/op-dev/config/multi-ns-install.yaml

### Uninstall

> kubectl delete -f config/multi-ns-install.yaml