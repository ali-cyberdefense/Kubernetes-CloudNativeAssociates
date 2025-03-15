## Setting Up EKS (Elastic Kubernetes Service)

**Code:**

```python

# 1. Install Kubectl:

https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html

# 2. Install eksctl:

https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html


Install awscli :
# Add iam role permission for clusters

CREATE CLUSTER WITH COMMAND :

eksctl create cluster --name depoly-App-cluster --version 1.27 --region us-east-2 --nodegroup-name App-nodes --node-type t2.micro --nodes 2
--nodes-min 1 --nodes-max 4 --managed

#Create a Deployment:
Create a YAML file, e.g., nginx-deployment.yaml, with the following content:


apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
	matchLabels:
  	app: nginx
  template:
	metadata:
  	labels:
    	app: nginx
	spec:
  	containers:
  	- name: nginx
    	image: nginx:latest
    	ports:
    	- containerPort: 80



kubectl apply -f nginx-deployment.yaml

Kubectl get pods .

```
### Creating Cluster on EKS
![Code Execution](https://i.imgur.com/H0S2b8k.png)

### Active Cluster
![Code Execution](https://i.imgur.com/bfi2BmN.png)

### Creating Nodes
![Code Execution](https://i.imgur.com/J3DoOOj.png)

### Active Nodes
![Code Execution](https://i.imgur.com/AHGeP4C.png)

### Deployment & Pods
![Code Execution](https://i.imgur.com/tE0dTEo.png)
