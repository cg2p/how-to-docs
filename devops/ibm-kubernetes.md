# Kubes 

## finding services

kubectl config current-context
kubectl get namespace

kubectl get services --all-name                         
kubectl get pods --all-namespaces

> in context of ibm cloud kubes cluster
kubectl create secret generic echo-service-url --from-literal=echo_service_url=http://173.193.79.169:32743 --namespace  prod 

 


## Connecting K8s app to IBM Cloud db
```
ibmcloud login

kubectl config current-context
kubectl config use-context swp-cluster/brab7k8d02k3fvrfrl00


# target where k8s cluster is e.g. resource group 'swp-dev'
ibmcloud target -g swp-dev 

# set cluster context
ibmcloud ks cluster config --cluster brab7k8d02k3fvrfrl00

# add private namespace for image registry
ibmcloud cr namespace-add swp-ns

# get namespaces in current cluster context
kubectl get namespace

# add the Cloud Databases deployment to your cluster
# syntax: ibmcloud ks cluster service bind --cluster CLUSTER --namespace NAMESPACE --service SERVICE
ibmcloud ks cluster service bind --cluster swp --namespace prod --service db-mongo-swp

# 
kubectl get secrets --namespace=prod
> shows list incl. secret just created 'binding-db-mongo-swp'

kubectl get secret --namespace=prod binding-db-mongo-swp