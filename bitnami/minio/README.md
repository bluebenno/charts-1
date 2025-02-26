# MinIO

[MinIO](https://min.io) is an object storage server, compatible with Amazon S3 cloud storage service, mainly used for storing unstructured data (such as photos, videos, log files, etc.)

## TL;DR;

```console
$ helm install bitnami/minio
```

## Introduction

This chart bootstraps a [MinIO](https://github.com/bitnami/bitnami-docker-minio) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters. This Helm chart has been tested on top of [Bitnami Kubernetes Production Runtime](https://kubeprod.io/) (BKPR). Deploy BKPR to get automated TLS certificates, logging and monitoring for your applications.

## Prerequisites

- Kubernetes 1.8+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release bitnami/minio
```

The command deploys MinIO on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the MinIO chart and their default values.

| Parameter                              | Description                                                                                  | Default                                                 |
| ---------------------------------------| -------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| `global.imageRegistry`                 | Global Docker image registry                                                                 | `nil`                                                   |
| `global.imagePullSecrets`              | Global Docker registry secret names as an array                                              | `[]` (does not add image pull secrets to deployed pods) |
| `global.minio.existingSecret`          | Name of existing secret to use for MinIO credentials (overrides `existingSecret`)            | `nil`                                                   |
| `global.minio.accessKey`               | MinIO Access Key (overrides `accessKey.password`)                                            | `nil`                                                   |
| `global.minio.secretKey`               | MinIO Secret Key (overrides `secretKey.password`)                                            | `nil`                                                   |
| `image.registry`                       | MinIO image registry                                                                         | `docker.io`                                             |
| `image.repository`                     | MinIO image name                                                                             | `bitnami/minio`                                         |
| `image.tag`                            | MinIO image tag                                                                              | `{TAG_NAME}`                                            |
| `image.pullPolicy`                     | Image pull policy                                                                            | `IfNotPresent`                                          |
| `image.pullSecrets`                    | Specify docker-registry secret names as an array                                             | `[]` (does not add image pull secrets to deployed pods) |
| `image.debug`                          | Specify if debug logs should be enabled                                                      | `false`                                                 |
| `clientImage.registry`                 | MinIO Client image registry                                                                  | `docker.io`                                             |
| `clientImage.repository`               | MinIO Client image name                                                                      | `bitnami/minio-client`                                  |
| `clientImage.tag`                      | MinIO Client image tag                                                                       | `{TAG_NAME}`                                            |
| `mode`                                 | MinIO server mode (`standalone` or `distributed`)                                            | `standalone`                                            |
| `statefulset.replicaCount`             | Number of pods (only for Minio distributed mode). Should be 4 <= x <= 32                     | `4`                                                     |
| `statefulset.updateStrategy`           | Statefulset update strategy policy                                                           | `RollingUpdate`                                         |
| `statefulset.podManagementpolicy`      | Statefulset pods management policy                                                           | `Parallel`                                              |
| `existingSecret`                       | Existing secret with MinIO credentials                                                       | `nil`                                                   |
| `useCredentialsFile`                   | Have the secret mounted as a file instead of env vars                                        | `false`                                                 |
| `accessKey.password`                   | MinIO Access Key. Ignored if existing secret is provided.                                    | _random 10 character alphanumeric string_               |
| `accessKey.forcePassword`              | Force users to specify an Access Key                                                         | `false`                                                 |
| `secretKey.password`                   | MinIO Secret Key. Ignored if existing secret is provided.                                    | _random 40 character alphanumeric string_               |
| `secretKey.forcePassword`              | Force users to specify an Secret Key                                                         | `false`                                                 |
| `defaultBuckets`                       | Comma, semi-colon or space separated list of buckets to create (only in standalone mode)     | `nil`                                                   |
| `disableWebUI`                         | Disable MinIO Web UI                                                                         | `false`                                                 |
| `extraEnv`                             | Any extra environment variables you would like to pass to the pods                           | `{}`                                                    |
| `podAnnotations`                       | Annotations to be added to pods                                                              | `{}`                                                    |
| `antiAffinity`                         | Pod anti-affinity policy                                                                     | `soft`                                                  |
| `nodeAffinity`                         | Node affinity policy                                                                         | `nil`                                                   |
| `resources`                            | Pod resources                                                                                | `{}`                                                    |
| `securityContext.enabled`              | Enable security context                                                                      | `true`                                                  |
| `securityContext.fsGroup`              | Group ID for the container                                                                   | `1001`                                                  |
| `securityContext.runAsUser`            | User ID for the container                                                                    | `1001`                                                  |
| `clusterDomain`                        | Kubernetes cluster domain                                                                    | `cluster.local`                                         |
| `livenessProbe.enabled`                | Enable/disable the Liveness probe                                                            | `true`                                                  |
| `livenessProbe.initialDelaySeconds`    | Delay before liveness probe is initiated                                                     | `60`                                                    |
| `livenessProbe.periodSeconds`          | How often to perform the probe                                                               | `10`                                                    |
| `livenessProbe.timeoutSeconds`         | When the probe times out                                                                     | `5`                                                     |
| `livenessProbe.successThreshold`       | Minimum consecutive successes for the probe to be considered successful after having failed. | `1`                                                     |
| `livenessProbe.failureThreshold`       | Minimum consecutive failures for the probe to be considered failed after having succeeded.   | `6`                                                     |
| `readinessProbe.enabled`               | Enable/disable the Readiness probe                                                           | `true`                                                  |
| `readinessProbe.initialDelaySeconds`   | Delay before readiness probe is initiated                                                    | `5`                                                     |
| `readinessProbe.periodSeconds`         | How often to perform the probe                                                               | `10`                                                    |
| `readinessProbe.timeoutSeconds`        | When the probe times out                                                                     | `5`                                                     |
| `readinessProbe.failureThreshold`      | Minimum consecutive failures for the probe to be considered failed after having succeeded.   | `6`                                                     |
| `readinessProbe.successThreshold`      | Minimum consecutive successes for the probe to be considered successful after having failed. | `1`                                                     |
| `persistence.enabled`                  | Use a PVC to persist data                                                                    | `true`                                                  |
| `persistence.mountPath`                | Path to mount the volume at                                                                  | `/data`                                                 |
| `persistence.storageClass`             | Storage class of backing PVC                                                                 | `nil` (uses alpha storage class annotation)             |
| `persistence.accessMode`               | Use volume as ReadOnly or ReadWrite                                                          | `ReadWriteOnce`                                         |
| `persistence.size`                     | Size of data volume                                                                          | `8Gi`                                                   |
| `persistence.annotations`              | Persistent Volume annotations                                                                | `{}`                                                    |
| `persistence.existingClaim`            | Name of an existing PVC to use (only in "standalone" mode)                                   | `nil`                                                   |
| `service.type`                         | Kubernetes Service type                                                                      | `ClusterIP`                                             |
| `service.port`                         | MinIO service port                                                                           | `9000`                                                  |
| `service.nodePort`                     | Port to bind to for NodePort service type                                                    | `nil`                                                   |
| `service.loadBalancerIP`               | Static IP Address to use for LoadBalancer service type                                       | `nil`                                                   |
| `service.annotations`                  | Kubernetes service annotations                                                               | `{}`                                                    |
| `ingress.certManager`                  | Add annotations for cert-manager                                                             | `false`                                                 |
| `ingress.annotations`                  | Ingress annotations                                                                          | `[]`                                                    |
| `ingress.hosts[0].name`                | Hostname to your MinIO installation                                                          | `minio.local`                                           |
| `ingress.hosts[0].path`                | Path within the url structure                                                                | `/`                                                     |
| `ingress.tls[0].hosts[0]`              | TLS hosts                                                                                    | `minio.local`                                           |
| `ingress.tls[0].secretName`            | TLS Secret (certificates)                                                                    | `minio.local-tls`                                       |
| `ingress.secrets[0].name`              | TLS Secret Name                                                                              | `nil`                                                   |
| `ingress.secrets[0].certificate`       | TLS Secret Certificate                                                                       | `nil`                                                   |
| `ingress.secrets[0].key`               | TLS Secret Key                                                                               | `nil`                                                   |
| `networkPolicy.enabled`                | Enable NetworkPolicy                                                                         | `false`                                                 |
| `networkPolicy.allowExternal`          | Don't require client label for connections                                                   | `true`                                                  |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set accessKey.password=minio-access-key \
  --set secretKey.password=minio-secret-key \
    bitnami/minio
```

The above command sets the MinIO Server access key and secret key to `minio-access-key` and `minio-secret-key`, respectively.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml bitnami/minio
```

> **Tip**: You can use the default [values.yaml](values.yaml)

### Production configuration

This chart includes a `values-production.yaml` file where you can find some parameters oriented to production configuration in comparison to the regular `values.yaml`.

```console
$ helm install --name my-release -f ./values-production.yaml bitnami/minio
```

- MinIO server mode:
```diff
- mode: standalone
+ mode: distributed
```

- Disable MinIO Web UI:
```diff
- disableWebUI: false
+ disableWebUI: true
```

- Annotations to be added to pods:
```diff
- podAnnotations: {}
+ podAnnotations:
+   prometheus.io/scrape: "true"
+   prometheus.io/path: "/minio/prometheus/metrics"
+   prometheus.io/port: "9000"
```

- Pod resources:
```diff
- resources: {}
+ resources:
+   requests:
+     memory: 256Mi
+     cpu: 250m
```

- Enable NetworkPolicy:
```diff
- networkPolicy.enabled: false
+ networkPolicy.enabled: true
```

- Don't require client label for connections:
```diff
- networkPolicy.allowExternal: true
+ networkPolicy.allowExternal: false
```

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

## Distributed mode

You can start the MinIO chart in distributed mode with the following command:

```console
$ helm install --name my-release bitnami/minio --set mode=distributed
```

This chart sets Minio server in distributed mode with 4 nodes by default. You can change the number of nodes setting the `statefulset.replicaCount` parameter:

```console
$ helm install --name my-release bitnami/minio --set mode=distributed --set statefulset.replicaCount=8
```

> Note: that the number of replicas must even, greater than 4 and lower than 32

## Prometheus exporter

MinIO exports Prometheus metrics at `/minio/prometheus/metrics`. To allow Prometheus collecting your MinIO metrics, modify the `values.yaml` adding the corresponding annotations:

```diff
- podAnnotations: {}
+ podAnnotations:
+   prometheus.io/scrape: "true"
+   prometheus.io/path: "/minio/prometheus/metrics"
+   prometheus.io/port: "9000"
```

> Find more information about MinIO metrics at https://docs.min.io/docs/how-to-monitor-minio-using-prometheus.html

## Persistence

The [Bitnami MinIO](https://github.com/bitnami/bitnami-docker-minio) image stores data at the `/data` path of the container.

The chart mounts a [Persistent Volume](http://kubernetes.io/docs/user-guide/persistent-volumes/) at this location. The volume is created using dynamic volume provisioning.
