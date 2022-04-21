# Lets LoadBalance
🔖 In kubernetes we have 4 types of networking services:
- ClusterIP -> Only Accessible within the cluster
- NodePort -> Expose the application directly to outside
- LoadBalancer -> Reach the application from ouside (Better security rather than NodePort)
- Ingress Controller -> Route traffic based on different DNS names to different apps

## MetalLB as a LoadBalancer
🔖 This is the solution that im going to use when im deploying kubernetes in local environment.

**NOTE**: When you are using a public cloud like AWS, GCP or Azure you definately dont need this solution.

➡️ [AWS ELB](https://aws.amazon.com/elasticloadbalancing/)

➡️ [GCP Load Balancer](https://cloud.google.com/load-balancing)

➡️ [Azure Load Balancer](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview)

➡️ [MetalLB](https://metallb.universe.tf/installation/)
