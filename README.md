# Sablier Kubernetes Helm Charts

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/sablier-helm-charts)](https://artifacthub.io/packages/search?repo=sablier-helm-charts)

The code is provided as-is with no warranties.

## Usage

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

The charts are published in two forms, and both are kept in sync by the same release job. Use whichever fits your tooling.

### OCI registry

Every chart is pushed to GitHub Container Registry as an [OCI artifact](https://helm.sh/docs/topics/registries/), under `oci://ghcr.io/sablierapp/helm-charts`. There is no repo to add — reference the chart by its URL:

```console
helm show chart oci://ghcr.io/sablierapp/helm-charts/sablier
helm install my-release oci://ghcr.io/sablierapp/helm-charts/sablier
```

Pass `--version` to pin a specific chart version. This requires Helm 3.8 or later, where OCI support is enabled by default.

Charts are GPG-signed and their provenance file is pushed alongside the chart, so `helm pull --verify` works once the maintainer's public key is in your keyring.

### Helm repository

```console
helm repo add sablier https://sablierapp.github.io/helm-charts
```

You can then run `helm search repo sablier` to see the charts.

<!-- Keep full URL links to repo files because this README syncs from main to gh-pages.  -->
Chart documentation is available in [sablier directory](https://github.com/sablierapp/helm-charts/blob/main/charts/sablier/README.md).

## Contributing

<!-- Keep full URL links to repo files because this README syncs from main to gh-pages.  -->
We'd love to have you contribute! Please refer to our [contribution guidelines](https://github.com/sablierapp/helm-charts/blob/main/CONTRIBUTING.md) for details.

## License

<!-- Keep full URL links to repo files because this README syncs from main to gh-pages.  -->
[Apache 2.0 License](https://github.com/sablierapp/helm-charts/blob/main/LICENSE).