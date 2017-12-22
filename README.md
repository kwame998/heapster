# Heapster

[![GoDoc](https://godoc.org/k8s.io/heapster?status.svg)](https://godoc.org/k8s.io/heapster) [![Build Status](https://travis-ci.org/kubernetes/heapster.svg?branch=master)](https://travis-ci.org/kubernetes/heapster)  [![Go Report Card](https://goreportcard.com/badge/github.com/kubernetes/heapster)](https://goreportcard.com/report/github.com/kubernetes/heapster)

Heapster enables Container Cluster Monitoring and Performance Analysis for [Kubernetes](https://github.com/kubernetes/kubernetes) (versions v1.0.6 and higher), and platforms which include it.

Heapster collects and interprets various signals like compute resource usage, lifecycle events, etc.
Note that the model API, formerly used provide REST access to its collected metrics, is now deprecated.
Please see [the model documentation](docs/model.md) for more details.

Heapster supports multiple sources of data.
More information [here](docs/source-configuration.md).

Heapster supports the pluggable storage backends described [here](docs/sink-owners.md).
We welcome patches that add additional storage backends.
Documentation on storage sinks [here](docs/sink-configuration.md).
The current version of Storage Schema is documented [here](docs/storage-schema.md).

### Running Heapster on Kubernetes

Heapster can run on a Kubernetes cluster using a number of backends.  Some common choices:
- [InfluxDB](docs/influxdb.md)
- [Stackdriver Monitoring and Logging](docs/google.md) for Google Cloud Platform
- [Other backends](docs/)

### Running Heapster on OpenShift

Using Heapster to monitor an OpenShift cluster requires some additional changes to the Kubernetes instructions to allow communication between the Heapster instance and OpenShift's secured endpoints. To run standalone Heapster or a combination of Heapster and Hawkular-Metrics in OpenShift, follow [this guide](https://github.com/openshift/origin-metrics).

#### Troubleshooting guide [here](docs/debugging.md)


## Community

Contributions, questions, and comments are all welcomed and encouraged! Developers hang out on [Slack](https://kubernetes.slack.com) in the #sig-instrumentation channel (get an invitation [here](http://slack.kubernetes.io/)). We also have the [kubernetes-dev Google Groups mailing list](https://groups.google.com/forum/#!forum/kubernetes-dev). If you are posting to the list please prefix your subject with "heapster: ".


git clone https://github.com/kubernetes/heapster

cd heapster

kubectl create -f deploy/kube-config/influxdb/

kubectl create -f deploy/kube-config/rbac/heapster-rbac.yaml

稍等一会，就可以通过kubectl cluster-info看到这些服务：
$ kubectl cluster-info

kubectl proxy --address='0.0.0.0' --port=8080 --accept-hosts='^*$' &


http://<master-ip>:8080/api/v1/proxy/namespaces/kube-system/services/monitoring-grafana
