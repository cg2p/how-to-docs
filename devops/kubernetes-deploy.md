# Multicloud DevOps steps
Capture the command line steps to perfom e2e build and deploy to different cloud and Kubernetes environments

Pre-requisite CLI tools
- kubectl
- ibmcloud
- oc
- odo

Pattern
- start kuberetes system (if local)
- set kubernetes context
- log into cloud system
- create kuberentes cluster
- create additional services e.g. database
- create service bindings (secrets)
- build docker images
- deploy to k8s cluster
- destroy cluster and db


## IBM Cloud
### 1. Create Cluster
```
# login to IBM Cloud
ibmcloud login -a cloud.ibm.com -r us-south --sso
> one time code
> select an account e.g. 2. Greg Hintermeister's Account (b71ac2564ef0b98f1032d189795994dc) <-> 1583351

# target resource group
ibmcloud target -g Guest-Clusters

# create free cluster and tag it
ibmcloud ks cluster create classic --name caine-iks-free 
> Cluster created with ID brcbsvrd0ae42godg6pg

# tag
ibmcloud ks cluster ls
ibmcloud resource tag-attach --tag-names caine --resource-name caine-iks-free
ibmcloud resource tags | grep caine

# wait for cluster to deploy then set the kubernetes context
ibmcloud ks cluster config --cluster brcbsvrd0ae42godg6pg

# verify you can connect to the cluster
kubectl config current-context
```

### 2. Create Database
From the catalogue page https://cloud.ibm.com/catalog/services/databases-for-mongodb
name: `caine-mongodb`
```
ibmcloud resource tag-attach --tag-names caine --resource-name caine-mongodb
```
IBM Cloud
- created db instance `caine-mongodb` in target 'Guest-Cluster'
- Manage tab > Settings > change Admin pwd
- Service Credentials > Create New `caine-mongodb-service-credential`

Compass
- https://cloud.ibm.com/docs/databases-for-mongodb?topic=databases-for-mongodb-getting-started
- connection, paste in 'composed' as URI string, the one starting 'mongodb://'
- fill in connection settings manually
- create a cert file using TLS Certificate | Content 
- More Options | Server Validated | use cert file

```
ibmcloud ks cluster service bind caine-iks-free Guest-Cluster caine-mongodb
```

### 3. Bind Service to Cluster
```
# create a namespace for your cluster
kubectl create namespace caine-echo-ns

# bind the database service to the cluster into a secret
ibmcloud ks cluster service bind --cluster caine-iks-free --namespace caine-echo-ns --service caine-mongodb
kubectl get secrets -n caine-echo-ns

```

## X. Delete Cleanup
```
# list cluster
ibmcloud ks cluster ls

# delete cluster
ibmcloud ks cluster rm --cluster caine-iks-free
```