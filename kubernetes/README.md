# k8s with Helm Chart 

This Helm chart deploys a monitoring stack including Krakend, Prometheus, Grafana, and Jaeger.

## Overview

This chart sets up the following components:
- **Krakend**: An API Gateway that manages API requests and aggregates responses.
- **Prometheus**: A monitoring and alerting toolkit.
- **Grafana**: A visualization tool for dashboards and metrics.
- **Jaeger**: A distributed tracing system.

## Prerequisites

- Kubernetes cluster (minikube, GKE, EKS, etc.)
- Helm 3.x
- kubectl

## Installation

1. **Clone the repository:**

   ```
   git clone https://github.com/Kavindu-Jayasinghe/krakend-with-grafana-prometheus-and-jaeger-microservices.git
   cd /krakend-with-grafana-prometheus-and-jaeger-microservices/kubernetes/helm
   ```
2. ** Package the Helm chart:**
```
helm package .

```
3. ** Add your chart to Helm repository (optional):**
```
helm repo index ./ --url https://your-repo-url/

```
4. **Install the chart:**
```
helm install my-monitoring-stack ./your-chart-1.0.0.tgz --values values.yaml

```

# Manually Creating ConfigMaps
If you prefer to create the ConfigMaps manually before deploying the chart, you can use the following kubectl commands:
## Krakend ConfigMap
switch the location where your krakend.json
```
kubectl create configmap krakend-config --from-file=krakend.json

```
## Prometheus ConfigMap
switch the location where your prometheus.yml
```
kubectl create configmap prometheus-config --from-file=prometheus.yml

```
## Grafana Datasources ConfigMap
switch the location where your datasource.yaml
```
kubectl create configmap grafana-datasources --from-file=datasources.yaml

```
## Grafana Provisioning ConfigMap
switch the location where your all.yaml
```
kubectl create configmap grafana-provisioning --from-file=all.yml

```
