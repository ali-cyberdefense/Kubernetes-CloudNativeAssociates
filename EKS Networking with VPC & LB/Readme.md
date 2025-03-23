## EKS Networking with VPC and Load Balancer

### Step#1: Set up a VPC for EKS

**Code:**

```python
eksctl create cluster --name depoly-cluster --version 1.27 --region us-east-2 --nodegroup-name App-nodes --node-type  t3.micro --nodes 2 --nodes-min 1 --nodes-max 4 --managed
```
**Cluster Cretion:**

![Code Execution](https://i.imgur.com/h7joG5v.png)


### Step#2: Deploy your application to the cluster using Kubernetes manifest

**Code:**

```python
# Example deployment.yaml for a sample application
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sample-app
spec:
  replicas: 3
  selector:
	matchLabels:
  	app: sample-app
  template:
	metadata:
  	labels:
    	app: sample-app
	spec:
  	containers:
    	- name: sample-app
      	image: <your-container-image>
      	ports:
        	- containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: sample-app-service
spec:
  selector:
	app: sample-app
  ports:
	- protocol: TCP
  	port: 80
  	targetPort: 80
  type: LoadBalancer

kubectl apply -f deployment.yaml
```
**Deployment and Service Creation:**

![Code Execution](https://i.imgur.com/VOUQQe4.png)


### Step#3: Test Connectivity and Load Balancing

**Code:**

```python
kubectl get svc sample-app-service

curl http://<external-ip>
```
**Successfully Connected**

![Code Execution](https://i.imgur.com/4aDS0Js.png)



