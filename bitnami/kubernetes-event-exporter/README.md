# kubernetes-event-exporter

[kubernetes-event-exporter](https://github.com/opsgenie/kubernetes-event-exporter) allows exporting the often missed Kubernetes events to various outputs so that they can be used for observability or alerting purposes.

## TL;DR

```console
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm install my-release bitnami/kubernetes-event-exporter
```

## Introduction

This chart bootstraps a [kubernetes-event-exporter](https://github.com/opsgenie/kubernetes-event-exporter) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.


## Prerequisites

- Kubernetes 1.12+
- Helm 2.11+ or Helm 3.0-beta3+

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm install my-release bitnami/kubernetes-event-exporter
```

These commands deploy kubernetes-event-exporter on the Kubernetes cluster in the default configuration. The [Parameters](##parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list` or `helm ls --all-namespaces`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the Kubernetes Event Exporter chart and their default values.

| Parameter                               | Description                                                                                        | Default                                                    |
|-----------------------------------------|----------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `affinity`                              | Affinity for pod assignment                                                                        | `{}` (evaluated as a template)                             |
| `config.logFormat`                      | How the logs are formatted. Allowed values: `pretty` or `json`                                     | `"pretty"`                                                 |
| `config.logLevel`                       | Verbosity of the logs (options: `fatal`, `error`, `warn`, `info` or `debug`)                       | `"debug"`                                                  |
| `config.receivers`                      | Array containing event receivers                                                                   | `[ {"name": "dump", "file": { "path": "/dev/stdout" }} ]`  |
| `config.route.routes`                   | Array containing event route configuration                                                         | `[ {"match": [ {"receiver": "dumps"} ]} ]`                 |
| `extraEnvVars`                          | Array containing extra env vars to be added to all containers                                      | `[]` (evaluated as a template)                             |
| `extraEnvVarsConfigMap`                 | ConfigMap containing extra env vars to be added to all containers                                  | `""` (evaluated as a template)                             |
| `extraEnvVarsSecret`                    | Secret containing extra env vars to be added to all containers                                     | `""` (evaluated as a template)                             |
| `extraVolumeMounts`                     | Array to add extra mounts (normally used with extraVolumes)                                        | `[]`                                                       |
| `extraVolumes`                          | Array to add extra volumes                                                                         | `[]`                                                       |
| `image.pullPolicy`                      | Container image pull policy                                                                        | `"IfNotPresent"`                                           |
| `image.registry`                        | Container image registry                                                                           | `"docker.io"`                                              |
| `image.repository`                      | Container image name                                                                               | `"opsgenie/kubernetes-event-exporter"`                     |
| `image.tag`                             | Container image tag                                                                                | `0.9`                                                      |
| `initContainers`                        | Attach additional init containers to pods                                                          | `[]` (evaluated as a template)                             |
| `nodeAffinityPreset.key`                | Node label key to match. Ignored if `affinity` is set.                                             | `""`                                                       |
| `nodeAffinityPreset.type`               | Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard`          | `""`                                                       |
| `nodeAffinityPreset.values`             | Node label values to match. Ignored if `affinity` is set.                                          | `[]`                                                       |
| `nodeSelector`                          | Node labels for pod assignment                                                                     | `{}`                                                       |
| `podAffinityPreset`                     | Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                | `""`                                                       |
| `podAnnotations`                        | Pod annotations                                                                                    | `{}`                                                       |
| `podAntiAffinityPreset`                 | Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`           | `"soft"`                                                   |
| `podSecurityContext`                    | Pod securityContext                                                                                | `{}`                                                       |
| `rbac.create`                           | Create the RBAC roles for API accessibility                                                        | `true`                                                     |
| `resources.limits`                      | Specify resource limits which the container is not allowed to succeed.                             | `{}`                                                       |
| `resources.requests`                    | Specify resource requests which the container needs to spawn.                                      | `{}`                                                       |
| `securityContext.capabilities.drop`     | Drop capabilities for the securityContext                                                          | `["ALL"]`                                                  |
| `securityContext.capabilities.add`      | Add capabilities for the securityContext                                                           | `[]`                                                       |
| `securityContext.readOnlyRootFilesystem`| Allows the pod to mount the RootFS as ReadOnly only                                                | `true`                                                     |
| `securityContext.runAsNonRoot`          | If the pod should run as a non root container.                                                     | `true`                                                     |
| `securityContext.runAsUser`             | Define the uid with which the pod will run                                                         | `1000`                                                     |
| `serviceAccount.create`                 | Create a serviceAccount for the pod                                                                | `true`                                                     |
| `serviceAccount.name`                   | Use the serviceAccount with the specified name                                                     | `""`                                                       |
| `tolerations`                           | Tolerations for pod assignment                                                                     | `[]`                                                       |

## Configuration and installation details

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.