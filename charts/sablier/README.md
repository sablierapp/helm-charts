# sablier


![Version: 1.0.3](https://img.shields.io/badge/Version-1.0.3-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.8.1](https://img.shields.io/badge/AppVersion-1.8.1-informational?style=flat-square) 

A free and open-source software to start workloads on demand and stop them after a period of inactivity.

## Source Code

* <https://github.com/sablierapp/sablier>



## Get Repo Info

```console
helm repo add sablier https://sablierapp.github.io/helm-charts
helm repo update
```

_See [helm repo](https://helm.sh/docs/helm/helm_repo/) for command documentation._

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm install my-release sablier/sablier
```

## Uninstalling the Chart

To uninstall/delete the my-release deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Upgrading an existing Release to a new major version

A major chart version change (like v1.2.3 -> v2.0.0) indicates that there is an incompatible breaking change needing manual actions. Until this chart's version reaches `v1.0`, there are no promises of backwards compatibility.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| deploymentAnnotations | object | `{}` | Annotations for all deployed Deployments |
| deploymentLabels | object | `{}` | Labels for all deployed Deployments |
| deploymentStrategy | object | `{"rollingUpdate":{"maxSurge":"25%","maxUnavailable":"25%"},"type":"RollingUpdate"}` | Deployment strategy for all deployed Deployments |
| image.repository | string | `"sablierapp/sablier"` | Sablier image repository |
| image.tag | string | `""` | Sablier image tag (deafult) appVersion |
| imagePullPolicy | string | `"IfNotPresent"` | Sablier imagePullPolicy |
| livenessProbe | object | `{"failureThreshold":3,"httpGet":{"path":"/health","port":10000},"initialDelaySeconds":5,"periodSeconds":5,"successThreshold":1,"timeoutSeconds":1}` | Sablier livenessProbe |
| logLevel | string | `"trace"` | Sablier log level |
| podAnnotations | object | `{}` | Annotations for all deployed pods |
| podLabels | object | `{}` | Labels for all deployed pods |
| readinessProbe | object | `{"failureThreshold":3,"httpGet":{"path":"/health","port":10000},"initialDelaySeconds":5,"periodSeconds":5,"successThreshold":1,"timeoutSeconds":1}` | Sablier readinessProbe |
| replicas | int | `1` | Sablier's replicas |
| resources | object | `{}` | Resource limits and requests for sablier |