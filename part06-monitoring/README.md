# Monitoring The Cluster
This is one the most important topics in kubernete4s world. we MUST be aware of how our environment and infrastructure performs. The answer to this key is to deploy a monitoring solutiom.

There are many solutions out there to monitor our kubernetes cluster. Im going to demonstrate one of the bests.

## Prometheus + Grafana
📌 Prometheus: Prometheus is a free software application used for event monitoring and alerting. It records real-time metrics in a time series database built using a HTTP pull model, with flexible queries and real-time alerting.

📌 Grafana: Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources.

## Why should we monitor our kubernetes cluster ?
Effective monitoring for Kubernetes clusters makes it easier to manage your containerized infrastructure, by tracking uptime, utilization of cluster resources (such as memory, CPU, and storage), and interaction between cluster components.

## Lets Get Started
please make sure you understand the basic concepts of how to perform monitoring in our network environment.

### Step1: Deploy Prometheus
Its better to deploy prometheus in its own NameSpace. Deploying prometheus requiers :
- ConfigMap
- Secret
- ServiceAccount
- PVC
- Deployment
- ReplicaSet
- Pod
- DaemonSet
- RoleBinding

if you haven't deployed NFS Dynamic Provisionig yet, apply below coomand:
```
$ kubectl apply -f nfs-rbac.yml -f nfs-deployment.yml -f nfs-class.yml
```
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm inspect values prometheus-community/prometheus > /tmp/prometheus.values
```
Change values to your own match, Im goint to use service type: LoadBalancer and service port: 8080

```
$ helm install prometheus prometheus-community/prometheus --namespace prometheus --create-namespace --values /tmp/prometheus.values
```
### Step2: Deploy Grafana
```
$ helm repo add grafana https://grafana.github.io/helm-charts
$ helm inspect vaslues grafana/grafana > /tmp/grafana.values
```
Make sure to change ClusterIP to LoadBalancer or NodePort, then install grafana with :
```
$ helm install grafana grafana/grafana --namespace grafana --create-namespace --values /tmp/grafana.values
```