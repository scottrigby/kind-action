# *Kind* Action

A GitHub Action for Kubernetes IN Docker - local clusters for testing Kubernetes using [kubernetes-sigs/kind](https://kind.sigs.k8s.io/).

## Usage

### Pre-requisites

Create a workflow YAML file in your `.github/workflows` directory. An [example workflow](#example-workflow) is available below.
For more information, reference the GitHub Help Documentation for [Creating a workflow file](https://help.github.com/en/articles/configuring-a-workflow#creating-a-workflow-file).

### Inputs

For more information on inputs, see the [API Documentation](https://developer.github.com/v3/repos/releases/#input)

- `version`: The kind version to use (default: `v0.6.1`)
- `config`: The path to the kind config file
- `node_image`: The Docker image for the cluster nodes
- `cluster_name`: The name of the cluster to create (default: `chart-testing`)
- `wait`: The duration to wait for the control plane to become ready (default: `60s`)
- `log_level`: The log level for kind
- `install_local_path_provisioner`: If true, Rancher's local-path provisioner is installed which supports dynamic volume provisioning on multi-node clusters.
  The newly created local-path StorageClass is made the default.

### Example Workflow

Create a workflow (eg: `.github/workflows/create-cluster.yml`):

```yaml
name: Create Cluster

on: pull_request

jobs:
  create-cluster:
    runs-on: ubuntu-latest
    steps:
      - name: Create k8s Kind Cluster
        uses: helm/kind-action@v1.0.0-alpha.2
        with:
          install_local_path_provisioner: true
```

This uses [@helm/kind-action](https://www.github.com/helm/kind-action) GitHub Action to spin up a [kind](https://kind.sigs.k8s.io/) Kubernetes cluster on every Pull Request.
See [@helm/chart-testing-action](https://www.github.com/helm/chart-testing-action) for a more practical example.

## Code of conduct

Participation in the Helm community is governed by the [Code of Conduct](CODE_OF_CONDUCT.md).
