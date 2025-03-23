## Taking RDC to EC2-Ubuntu:

### Step1: Set up an EFS filesystem.

**EFS File System Creation**

![Code Execution](https://i.imgur.com/X2NVepJ.png)

### Step2: Installing CSI

**CSI Installed and in running stage**

![Code Execution](https://i.imgur.com/A8ClJN3.png)

![Code Execution](https://i.imgur.com/LIa4cM7.png)


### Step3: Creating Storage Class(SC) and Persistent Volume Claim(PVC)


```python

# FOR SC

apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: efs-sc
provisioner: efs.csi.aws.com
parameters:
  fsid: <YOUR_EFS_FILE_SYSTEM_ID>
  provisioningMode: efs

# FOR PVC
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: efs-pvc
spec:
  accessModes:
	- ReadWriteOnce
  resources:
	requests:
  	storage: 1Gi
  storageClassName: efs-sc

```
![Code Execution](https://i.imgur.com/3VUR8AO.png)


### Step4: Final Deployment

```python

apiVersion: apps/v1
kind: Deployment
metadata:
  name: efs-deployment1
spec:
  replicas: 2
  selector:
	matchLabels:
  	app: efs-deployment
  template:
	metadata:
  	labels:
    	app: efs-deployment
	spec:
  	containers:
  	- name: efs-container
    	image: nginx:latest
    	volumeMounts:
    	- name: efs-volume
      	mountPath: /efs
  	volumes:
  	- name: efs-volume
    	persistentVolumeClaim:
      	claimName: efs-pvc
```

![Code Execution](https://i.imgur.com/3OhYZ87.png)
