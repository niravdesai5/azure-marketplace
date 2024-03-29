# Odoo

[Odoo](https://www.odoo.com/) is a suite of web-based open source business apps. The main Odoo Apps include an Open Source CRM, Website Builder, eCommerce, Project Management, Billing & Accounting, Point of Sale, Human Resources, Marketing, Manufacturing, Purchase Management, ...

Odoo Apps can be used as stand-alone applications, but they also integrate seamlessly so you get a full-featured Open Source ERP when you install several Apps.

## Azure-ready Charts with Containers from marketplace.azurecr.io

This Helm Chart has been configured to pull the Container Images from the Azure Marketplace Public Repository.
The following command allows you to download and install all the charts from this repository.
```bash
$ helm repo add bitnami-azure https://marketplace.azurecr.io
```
## TL;DR;

```console
$ helm install bitnami-azure/odoo
```

## Introduction

This chart bootstraps a [Odoo](https://github.com/bitnami/bitnami-docker-odoo) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters. This chart has been tested to work with NGINX Ingress, cert-manager, fluentd and Prometheus on top of the [BKPR](https://kubeprod.io/).

## Prerequisites

- Kubernetes 1.4+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release bitnami-azure/odoo
```

The command deploys Odoo on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the Odoo chart and their default values.

| Parameter                             | Description                                               | Default                                                 |
|---------------------------------------|-----------------------------------------------------------|---------------------------------------------------------|
| `global.imageRegistry`                | Global Docker image registry                              | `nil`                                                   |
| `global.imagePullSecrets`             | Global Docker registry secret names as an array           | `[]` (does not add image pull secrets to deployed pods) |
| `image.registry`                      | Odoo image registry                                       | `docker.io`                                             |
| `image.repository`                    | Odoo Image name                                           | `bitnami/odoo`                                          |
| `image.tag`                           | Odoo Image tag                                            | `{TAG_NAME}`                                            |
| `image.pullPolicy`                    | Image pull policy                                         | `Always`                                                |
| `image.pullSecrets`                   | Specify docker-registry secret names as an array          | `[]` (does not add image pull secrets to deployed pods) |
| `nameOverride`                        | String to partially override odoo.fullname template with a string (will prepend the release name) | `nil`           |
| `fullnameOverride`                    | String to fully override odoo.fullname template with a string                                     | `nil`           |
| `odooUsername`                        | User of the application                                   | `user@example.com`                                      |
| `odooPassword`                        | Admin account password                                    | _random 10 character long alphanumeric string_          |
| `odooEmail`                           | Admin account email                                       | `user@example.com`                                      |
| `smtpHost`                            | SMTP host                                                 | `nil`                                                   |
| `smtpPort`                            | SMTP port                                                 | `nil`                                                   |
| `smtpUser`                            | SMTP user                                                 | `nil`                                                   |
| `smtpPassword`                        | SMTP password                                             | `nil`                                                   |
| `smtpProtocol`                        | SMTP protocol [`ssl`, `tls`]                              | `nil`                                                   |
| `service.type`                        | Kubernetes Service type                                   | `LoadBalancer`                                          |
| `service.port`                        | Service HTTP port                                         | `80`                                                    |
| `service.loadBalancer`                | Kubernetes LoadBalancerIP to request                      | `nil`                                                   |
| `service.externalTrafficPolicy`       | Enable client source IP preservation                      | `Cluster`                                               |
| `service.nodePort`                    | Kubernetes http node port                                 | `""`                                                    |
| `externalDatabase.host`               | Host of the external database                             | `localhost`                                             |
| `externalDatabase.user`               | Existing username in the external db                      | `postgres`                                              |
| `externalDatabase.password`           | Password for the above username                           | `nil`                                                   |
| `externalDatabase.database`           | Name of the existing database                             | `bitnami_odoo`                                          |
| `externalDatabase.port`               | Database port number                                      | `5432`                                                  |
| `ingress.enabled`                     | Enable ingress controller resource                        | `false`                                                 |
| `ingress.hosts[0].name`               | Hostname to your Odoo installation                        | `odoo.local`                                            |
| `ingress.hosts[0].path`               | Path within the url structure                             | `/`                                                     |
| `ingress.hosts[0].tls`                | Utilize TLS backend in ingress                            | `false`                                                 |
| `ingress.hosts[0].certManager`        | Add annotations for cert-manager                          | `false`                                                 |
| `ingress.hosts[0].tlsSecret`          | TLS Secret (certificates)                                 | `odoo.local-tls-secret`                                 |
| `ingress.hosts[0].annotations`        | Annotations for this host's ingress record                | `[]`                                                    |
| `ingress.secrets[0].name`             | TLS Secret Name                                           | `nil`                                                   |
| `ingress.secrets[0].certificate`      | TLS Secret Certificate                                    | `nil`                                                   |
| `ingress.secrets[0].key`              | TLS Secret Key                                            | `nil`                                                   |
| `resources`                           | CPU/Memory resource requests/limits                       | Memory: `512Mi`, CPU: `300m`                            |
| `persistence.enabled`                 | Enable persistence using PVC                              | `true`                                                  |
| `persistence.existingClaim`           | Enable persistence using an existing PVC                  | `nil`                                                   |
| `persistence.storageClass`            | PVC Storage Class                                         | `nil` (uses alpha storage class annotation)             |
| `persistence.accessMode`              | PVC Access Mode                                           | `ReadWriteOnce`                                         |
| `persistence.size`                    | PVC Storage Request                                       | `8Gi`                                                   |
| `postgresql.enabled`                  | Deploy PostgreSQL container(s)                            | `true`                                                  |
| `postgresql.postgresqlPassword`       | PostgreSQL password                                       | `nil`                                                   |
| `postgresql.persistence.enabled`      | Enable PostgreSQL persistence using PVC                   | `true`                                                  |
| `postgresql.persistence.storageClass` | PVC Storage Class for PostgreSQL volume                   | `nil` (uses alpha storage class annotation)             |
| `postgresql.persistence.accessMode`   | PVC Access Mode for PostgreSQL volume                     | `ReadWriteOnce`                                         |
| `postgresql.persistence.size`         | PVC Storage Request for PostgreSQL volume                 | `8Gi`                                                   |
| `livenessProbe.enabled`               | Enable/disable the liveness probe                         | `true`                                                  |
| `livenessProbe.initialDelaySeconds`   | Delay before liveness probe is initiated                  | 300                                                     |
| `livenessProbe.periodSeconds`         | How often to perform the probe                            | 30                                                      |
| `livenessProbe.timeoutSeconds`        | When the probe times out                                  | 5                                                       |
| `livenessProbe.failureThreshold`      | Minimum consecutive failures to be considered failed      | 6                                                       |
| `livenessProbe.successThreshold`      | Minimum consecutive successes to be considered successful | 1                                                       |
| `readinessProbe.enabled`              | Enable/disable the readiness probe                        | `true`                                                  |
| `readinessProbe.initialDelaySeconds`  | Delay before readinessProbe is initiated                  | 30                                                      |
| `readinessProbe.periodSeconds   `     | How often to perform the probe                            | 10                                                      |
| `readinessProbe.timeoutSeconds`       | When the probe times out                                  | 5                                                       |
| `readinessProbe.failureThreshold`     | Minimum consecutive failures to be considered failed      | 6                                                       |
| `readinessProbe.successThreshold`     | Minimum consecutive successes to be considered successful | 1                                                       |

The above parameters map to the env variables defined in [bitnami/odoo](http://github.com/bitnami/bitnami-docker-odoo). For more information please refer to the [bitnami/odoo](http://github.com/bitnami/bitnami-docker-odoo) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set odooPassword=password,postgresql.postgresPassword=secretpassword \
    bitnami-azure/odoo
```

The above command sets the Odoo administrator account password to `password` and the PostgreSQL `postgres` user password to `secretpassword`.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml bitnami-azure/odoo
```

> **Tip**: You can use the default [values.yaml](values.yaml)

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

## Persistence

The [Bitnami Odoo](https://github.com/bitnami/bitnami-docker-odoo) image stores the Odoo data and configurations at the `/bitnami/odoo` path of the container.

Persistent Volume Claims are used to keep the data across deployments. This is known to work in GCE, AWS, and minikube.
See the [Configuration](#configuration) section to configure the PVC or to disable persistence.

## Using an external database

Sometimes you may want to have Odoo connect to an external database rather than installing one inside your cluster, e.g. to use a managed database service, or use a single database server for all your applications. To do this, the chart allows you to specify credentials for an external database under the [`externalDatabase` parameter](#configuration). You should also disable the PostgreSQL installation with the `postgresql.enabled` option. For example:

```console
$ helm install bitnami-azure/odoo \
    --set postgresql.enabled=false,externalDatabase.host=myexternalhost,externalDatabase.user=myuser,externalDatabase.password=mypassword,externalDatabase.port=3306
```

Note also if you disable PostgreSQL per above you MUST supply values for the `externalDatabase` connection.

## Upgrading

### To 3.0.0

Backwards compatibility is not guaranteed unless you modify the labels used on the chart's deployments.
Use the workaround below to upgrade from versions previous to 3.0.0. The following example assumes that the release name is odoo:

```console
$ kubectl patch deployment odoo-odoo --type=json -p='[{"op": "remove", "path": "/spec/selector/matchLabels/chart"}]'
$ kubectl patch deployment odoo-postgresql --type=json -p='[{"op": "remove", "path": "/spec/selector/matchLabels/chart"}]'
```