# Getting Ready For Production
**In this section we are going to learn about kubernetes in production.**

🔖 Wen we are deploying a local kubernetes cluster in production environment we should consider some factors like:
- Amount of CPU, RAM nad Disk of the nodes.
- Number of master and worker nodes to match our need.
- Consider a good and reliable solution to provide storage to our applications.
- Setting up a Load Balancer for the pods.
- Understand how to route traffic to your apps from outside world.
- Security
- Observability (Monitoring and logs)
- Disaster recovery (Always have a plan to backup your cluster)
- Deployment velocity (using a CI/CD tool)
- Role Based Access Control (RBAC)

## What we are going to use
🔖 The Tools and services that we are going to use to cover these production factors are:
- MetalLB
- Rancher and Kubernetes Dashboard
- Prometheus and Grafana
- ELK and EFK stack
- Nginx Ingress Controller
- Jenkins
- Glusterfs and NFS
- Lets-Encrypt-CA

