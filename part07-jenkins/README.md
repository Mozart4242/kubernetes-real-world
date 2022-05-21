# Jenkins with kubernetes
Jenkins is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery. It is a server-based system that runs in servlet containers such as Apache Tomcat.

we are using Jenkins to deploy CI/CD in our infrastructure.

## How it works?
We can use Jenkins for sevral purposes. using it fot CI or just CD or Both CI/CD. Im going to explain here the most automated way to use Jenkins.

### scenario :
Developers team: are commiting changes and codes to Github.
DevOps team: deploy a automation way to pull that code into our CI platform, build that code, and if its successful deploy it in our infrastructure.

## Lets get started
Follow me with one of the most interesting and important topics in the DevOps.

### Step1: deploy Jnekins in k8s cluster
```
$ helm repo add jenkinsci https://charts.jenkins.io
$ helm repo update
$ helm inspect values jenkinsci/jenkins > /tmp/jenkins.values
$ helm install jenkins jenkinsci/jenkins --namespace jenkins --values /tmp/jenkins.values
```

### Step2: Configure Jenkins
Now we need to configure Jenkins to connect to our kubernetes cluster.

- Login to Jenkins Web UI
- Head to:
  - Manage Jenkins -> manage Credentials -> Jenkins -> Global Credentials -> Add Credential -> kind -> kubernetes service account
