# Ingress Controller
➕ In kubernetes we have 4 types of networking services:

ClusterIP -> Only Accessible within the cluster

NodePort -> Expose the application directly to outside

LoadBalancer -> Reach the application from ouside (Better security rather than NodePort)

**Ingress Controller -> Route traffic based on different DNS names to different apps**

## Nginx as an Ingress Controller
➕ An Ingress controller is a specialized load balancer for Kubernetes (and other containerized) environments. Kubernetes is the de facto standard for managing containerized applications.

➕ For many enterprises, moving production workloads into Kubernetes brings additional challenges and complexities around application traffic management. An Ingress controller abstracts away the complexity of Kubernetes application traffic routing and provides a bridge between Kubernetes services and external ones.

➕ Kubernetes Ingress controllers:

- Accept traffic from outside the Kubernetes platform, and load balance it to pods (containers) running inside the platform
- Can manage egress traffic within a cluster for services which need to communicate with other services outside of a cluster
- Are configured using the Kubernetes API to deploy objects called “Ingress Resources”
- Monitor the pods running in Kubernetes and automatically update the load‑balancing rules when pods are added or removed from a service

## Lets Get Started
Iam going to install Nginx Ingress-Controller from [kubernetes offical nginx ingress controller](https://kubernetes.github.io/ingress-nginx/deploy/).

### Step1 - Install nginx-ingress-controller using Helm
```
$ helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
$ helm repo update
```
Download values file to your machine and make some changes:
- Change to "kind: DaemonSet"
```
$ helm show values nginx-ingress/ingress-nginx > /tmp/nginx-ingress.yml

$ helm install ingress-nginx nginx-ingress/ingress-nginx --namespace ingress-nginx --create-namespace --values /tmp/nginx-ingress.yml

$ kubectl get all -n ingress-nginx
```

### Step2 - Create a sample nginx website

```
kubectl apply -f nginx-deploy-main.yml -f nginx-deploy-blue.yml
kubectl apply -f ingress-resource1.yml
```
Now open your web browser and visit : http://nginx.mozart4242.com and http://blue.nginx.mozart4242.com

NOTE: edit hosts file in your machine
```
echo "10.132.132.105 nginx.mozart4242.com blue.nginx.mozart4242.com" >> /etc/hosts
```
