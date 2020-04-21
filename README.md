# Helm Chart for ReDoc

## Introduction

This [Helm](https://github.com/kubernetes/helm) chart installs [redoc](https://github.com/Redocly/redoc/tree/master/config/docker) in a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster 1.15+
- Helm 3.1.1+

## Installation

### Configure the chart

The following items can be set via `--set` flag during installation or configured by editing the `values.yaml` directly (need to download the chart first).

#### Configure the way how to expose redoc service:

- **Ingress**: The ingress controller must be installed in the Kubernetes cluster.
- **ClusterIP**: Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster.
- **NodePort**: Exposes the service on each Node’s IP at a static port (the NodePort). You’ll be able to contact the NodePort service, from outside the cluster, by requesting `NodeIP:NodePort`.
- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer.

### Install the chart

Install the redoc helm chart with a release name `my-release`:

```bash
helm install --name my-release ./
```

## Uninstallation

To uninstall/delete the `my-release` deployment:

```bash
helm delete my-release
```

## Configuration

The following table lists the configurable parameters of the ReDoc chart and the default values.

| Parameter                                                                   | Description                                                                                                        | Default                         |
| --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------| ------------------------------- |
| **Image**                                                                   |
| `image.repository`                                                          | redoc Image name                                                                                              | `redocly/redoc`         |
| `image.tag`                                                                 | redoc Image tag                                                                                               | `v2.0.0-rc.27`                      |
| `image.pullPolicy`                                                          | redoc Image pull policy                                                                                       | `IfNotPresent`                  |
| **redoc**                                                              |
| `redoc.jsonPath`                                                       | location of the configuration json file file                                                                       | `""`                            |
| `redoc.jsonUrl`                                                        | location of the configuration json file file                                                                       | `http://petstore.swagger.io/v2/swagger.json` |
| **Service**                                                                 |
| `service.type`                                                              | Type of service for redoc frontend                                                                            | `NodePort`                      |
| `service.port`                                                              | Port to expose service                                                                                             | `80`                          |
| `service.nodePort`                                                          | Port where the service is reachable                                                                                | `30245`                         |
| `service.loadBalancerIP`                                                    | LoadBalancerIP if service type is `LoadBalancer`                                                                   | `nil`                           |
| `service.loadBalancerSourceRanges`                                          | Address that are allowed when svc is `LoadBalancer`                                                                | `[]`                            |
| `service.annotations`                                                       | Service annotations                                                                                                | `{}`                            |
| **Ingress**                                                                 |
| `ingress.enabled`                                                           | Enables Ingress                                                                                                    | `false`                         |
| `ingress.annotations`                                                       | Ingress annotations                                                                                                | `{}`                            |
| `ingress.path`                                                              | Path to access frontend                                                                                            | `/`                             |
| `ingress.hosts`                                                             | Ingress hosts                                                                                                      | `[]`                            |
| `ingress.tls`                                                               | Ingress TLS configuration                                                                                          | `[]`                            |
| **ReadinessProbe**                                                          |
| `readinessProbe`                                                            | Rediness Probe settings                                                                                            | `nil`                           |
| **LivenessProbe**                                                           | 
| `livenessProbe.httpGet.path`                                                | Liveness Probe settings                                                                                            | `/`                             |
| `livenessProbe.httpGet.port`                                                | Liveness Probe settings                                                                                            | `http`                          |
| `livenessProbe.initialDelaySeconds`                                         | Liveness Probe settings                                                                                            | `60`                            |
| `livenessProbe.periodSeconds`                                               | Liveness Probe settings                                                                                            | `30`                            |
| `livenessProbe.timeoutSeconds`                                              | Liveness Probe settings                                                                                            | `10`                            |
| **Resources**                                                               |
| `resources`                                                                 | CPU/Memory resource requests/limits                                                                                | `{}`                            |

## Contributing

Feel free to contribute by making a [pull request](https://github.com/SergeSpinoza/helm-redoc/pull/new/master).

Please read the official [Contribution Guide](https://github.com/helm/charts/blob/master/CONTRIBUTING.md) from Helm for more information on how you can contribute to this Chart.


