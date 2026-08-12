# sablier

![Version: 1.7.1](https://img.shields.io/badge/Version-1.7.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.1](https://img.shields.io/badge/AppVersion-1.16.1-informational?style=flat-square)

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

## Configuration

Sablier's own options go into the `config` value. The chart renders it into a ConfigMap and mounts it at `/etc/sablier/sablier.yml`, the first path Sablier searches at startup:

```yaml
config:
  provider:
    kubernetes:
      qps: 64
      burst: 128
  sessions:
    default-duration: 5m
  webhooks:
    endpoints:
      - url: https://uptime.example.com/api/push/xxxxxxxx
        events:
          - started
          - stopped
```

Every option from the [configuration reference](https://sablierapp.dev/reference/cli/) is accepted, including `webhooks`, which has no command-line flag.

Two keys behave differently. `provider.name` is passed as a command-line flag and setting it under `config` has no effect. `logging.level` defaults to the `logLevel` value, and `config` overrides it.

Options passed through `extraArgs` or `extraEnv` also take precedence over the file. Changing `config` or `logLevel` restarts the pods, because the pod template carries a checksum of the rendered file.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| config | object | `{}` | Sablier's configuration file, mounted at `/etc/sablier/sablier.yml` (see the Configuration section above) |
| deploymentAnnotations | object | `{}` | Annotations for all deployed Deployments |
| deploymentLabels | object | `{}` | Labels for all deployed Deployments |
| deploymentStrategy | object | `{"rollingUpdate":{"maxSurge":"25%","maxUnavailable":"25%"},"type":"RollingUpdate"}` | Deployment strategy for all deployed Deployments |
| extraArgs | list | `[]` | Extra CLI arguments appended to the sablier container args (e.g. - --server.metrics.enabled=true to expose Prometheus /metrics) |
| extraEnv | list | `[]` | Extra environment variables for the sablier container (e.g. TZ to control the local time used by `sablier.running-hours` windows) |
| extraVolumeMounts | list | `[]` | Extra volume mounts for the sablier container (e.g. to mount custom themes loaded via --strategy.dynamic.custom-themes-path) |
| extraVolumes | list | `[]` | Extra volumes for the sablier pod (e.g. a configMap volume with custom themes for --strategy.dynamic.custom-themes-path) |
| image.repository | string | `"sablierapp/sablier"` | Sablier image repository |
| image.tag | string | `""` | Sablier image tag (default) appVersion |
| imagePullPolicy | string | `"IfNotPresent"` | Sablier imagePullPolicy |
| livenessProbe | object | `{"failureThreshold":3,"httpGet":{"path":"/health","port":10000},"initialDelaySeconds":5,"periodSeconds":5,"successThreshold":1,"timeoutSeconds":1}` | Sablier livenessProbe |
| logLevel | string | `"info"` | Sablier log level, rendered as `logging.level` into the config file. A `logging.level` set under `config` takes precedence. |
| podAnnotations | object | `{}` | Annotations for all deployed pods |
| podLabels | object | `{}` | Labels for all deployed pods |
| rbac | object | `{"cnpg":false,"otkRedis":false}` | Sablier's RBAC Configuration |
| rbac.cnpg | bool | `false` | Enable CNPG integration necessary rights |
| rbac.otkRedis | bool | `false` | Enable OT-CONTAINER-KIT Redis operator necessary rights |
| readinessProbe | object | `{"failureThreshold":3,"httpGet":{"path":"/health","port":10000},"initialDelaySeconds":5,"periodSeconds":5,"successThreshold":1,"timeoutSeconds":1}` | Sablier readinessProbe |
| replicas | int | `1` | Sablier's replicas |
| resources | object | `{}` | Resource limits and requests for sablier |