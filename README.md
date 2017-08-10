# Grafana Helm Chart

This chart bootstraps an [Grafana](http://grafana.org) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

This is basically a fork of the CoreOS team's `grafana` chart.  See https://github.com/coreos/prometheus-operator/tree/master/helm/grafana

# Helm
We are using Helm along with Quay.io to host our Helm charts.  See https://github.com/app-registry/appr-helm-plugin and https://coreos.com/blog/quay-application-registry-for-kubernetes.html.

See https://docs.helm.sh for more about Helm.

# Prerequisites
* Kubernetes 1.4+ with Beta APIs enabled
* [Helm Registry plugin](https://github.com/app-registry/appr-helm-plugin)

# Installing this chart
To install with release name `my-release` run:
```
helm registry install quay.io/3dsim/grafana --name=my-release --set dataSourceURL=<url of prometheus to visualize>
```

# Uninstalling the Chart

To uninstall/delete the my-release deployment:
```
helm delete my-release
```
The command removes all the Kubernetes components associated with the chart and deletes the release.

# Configuration

Parameter | Description | Default
--- | --- | ---
`adminUser` | Grafana admin user name | `admin`
`adminPassword` | Grafana admin user password | `admin`
`dataSourceURL` | URL for prometheus instance to visualize | `""`
`image.repository` | Image | `grafana/grafana`
`image.tag` | Image tag | `4.4.1`
`ingress.enabled` | If true, Grafana Ingress will be created | `false`
`ingress.annotations` | Annotations for Grafana Ingress | `{}`
`ingress.fqdn` | Grafana Ingress fully-qualified domain name | `""`
`ingress.tls` | TLS configuration for Grafana Ingress | `[]`
`nodeSelector` | Node labels for pod assignment | `{}`
`resources` | Pod resource requests & limits | `{}`
`serverDashboardFiles` | key/value pairs of dashboard name to json defining the dashboard (see [example-kube-prometheus-values.yaml](example-kube-prometheus-values.yaml)) | `{}`
`service.annotations` | Annotations to be added to the Grafana Service | `{}`
`service.clusterIP` | Cluster-internal IP address for Grafana Service | `""`
`service.externalIPs` | List of external IP addresses at which the Grafana Service will be available | `[]`
`service.loadBalancerIP` | External IP address to assign to Grafana Service | `""`
`service.loadBalancerSourceRanges` | List of client IPs allowed to access Grafana Service | `[]`
`service.nodePort` | Port to expose Grafana Service on each node | `39093`
`service.type` | Grafana Service type | `ClusterIP`
`storageSpec` | Grafana StorageSpec for persistent data | `{}`

# Customizing this chart
See [values.yaml](values.yaml) for full configuration options.

Use `--set` syntax to set a value:
```console
helm registry install quay.io/3dsim/grafana --name=my-release --set resources.limits.cpu=300m
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
helm registry install quay.io/3dsim/grafana --name=my-release -f values.yaml
```

# Developers
Modify the chart and be sure to bump the version in [Chart.yaml](Chart.yaml).  After that, follow these directions to push the changes to Quay.io: https://github.com/app-registry/appr-helm-plugin#create-and-push-your-own-chart

Key instructions from the link:
```
helm registry login -u <your quay.io username> quay.io
helm registry push --namespace 3dsim quay.io
```