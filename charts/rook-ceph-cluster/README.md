# Rook CephCluster CRD Helm Chart

Rook allows creation and customization of storage clusters through the custom resource definitions (CRDs). This is a companion chart to Ceph Operator Helm Chart

- Ceph Operator Helm: https://rook.io/docs/rook/v1.5/helm-operator.html
- CephCluster CRD: https://rook.io/docs/rook/v1.5/ceph-cluster-crd.html

### Prerequisites

Install rook-ceph-operator and add this repo to your helm repositories

```bash
$ helm repo add mkhpalm https://mkhpalm.github.io/helm-charts/
$ helm repo update
```

What this chart does is manifests the cluster custom resource and adds a few things:

- RBAC to run CR in different namespaces than rook operator
- Ability to run multiple clusters from a single operator
- Ingress options for ceph manager
- Prometheus operator support to monitor metrics
- Alertmanager rules for ceph
- etc

### Configuration Options

You can define all configurations using `spec` just like the standalone CephCluster custom resource. If you are using multiple namespaces make sure to define `operator.namespace` so this chart knows how to map roles for rook-ceph-operator to access it.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0] | string | `"chart-example.local"` |  |
| ingress.path | string | `"/"` |  |
| ingress.tls | list | `[]` |  |
| operator.namespace | string | `"rook-ceph"` |  |
| serviceMonitor.enabled | bool | `false` |  |
| serviceMonitor.interval | string | `""` |  |
| serviceMonitor.metricRelabelings | list | `[]` |  |
| serviceMonitor.relabelings | list | `[]` |  |
| spec.cephVersion.image | string | `"ceph/ceph:v15.2.11"` |  |
| spec.dataDirHostPath | string | `"/var/lib/rook"` |  |
| spec.mon.allowMultiplePerNode | bool | `false` |  |
| spec.mon.count | int | `3` |  |
| spec.storage.useAllDevices | bool | `true` |  |
| spec.storage.useAllNodes | bool | `true` |  |
