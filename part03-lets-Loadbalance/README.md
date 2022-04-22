# Lets LoadBalance
➕ In kubernetes we have 4 types of networking services:
- ClusterIP -> Only Accessible within the cluster
- NodePort -> Expose the application directly to outside
- LoadBalancer -> Reach the application from ouside (Better security rather than NodePort)
- Ingress Controller -> Route traffic based on different DNS names to different apps

## MetalLB as a LoadBalancer
➕ This is the solution that im going to use when im deploying kubernetes in local environment.

**NOTE**: When you are using a public cloud like AWS, GCP or Azure you definitely dont need this solution.

➡️ [AWS ELB](https://aws.amazon.com/elasticloadbalancing/)

➡️ [GCP Load Balancer](https://cloud.google.com/load-balancing)

➡️ [Azure Load Balancer](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview)

➡️ [MetalLB](https://metallb.universe.tf/installation/)

## Lets Get Started

➕ What metallb is going to do for us is that it gives us specifed ip addresses within your nodes subnet.

➕ Im going to use just 5 ip addresses (10.132.132.105-10.132.132.110)

### Step1 - Prepration
check the Kube=proxy settings
```
$ kubectl edit configmap -n kube-system kube-proxy
```
if the mode is set to "ipvs" then change strictARP to "true:
```
apiVersion: kubeproxy.config.k8s.io/v1alpha1
kind: KubeProxyConfiguration
mode: "ipvs"
ipvs:
  strictARP: true
```

### Step2 - Installation
Install MetalLB with manifest

```
$ kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests/namespace.yaml
$ kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests/metallb.yaml
```

### Step3 - Verification

```
$ kubectl get ns
$ kubectl get all -n metallb-system
```

### Step4 - Configuration
Create a configMap to specify the ip addresses:

```
$ mkdir metallb && cd metallb

$ cat > configmap.yml <EOF
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 10.132.132.5-10.132.132.10
EOF

$ kubectl apply -f configmap.yml
```
### Step5 - Test
Lets create a nginx deployment and expose it as LoadBalancer

```
$ kubectl create deploy nginx --image nginx
$ kubectl expose deploy nginx --port 80 --type LoadBalancer

$ kubectl get all
```
Now open your web browser http://10.132.132.105.
