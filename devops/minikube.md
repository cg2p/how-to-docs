# Minikube

## Installation and Test
Install [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
```
brew install minikube
minikube start --vm-driver=hyperkit
kubectl version

kubectl get nodes
>NAME       STATUS   ROLES    AGE    VERSION
>minikube   Ready    master   2m9s   v1.18.0
```
Build and test a Hello World docker image
```
eval $(minikube docker-env)
docker run hello-world
```

## Minikube commands
```
minikube start
minikube version
kubectl config current-context
kubectl get node


```


## Build and deploy a test 3-tier application to Minikube
1. create a mongo db service
2. echo-service-with-mongo
3. echo-nextjs-client

### 1. Mongo database
hello

## Same again via Helm chart

docker build -t echo-service .
docker image ls
kubectl create -f manifest.yml
kubectl get deploy
kubectl apply -f service.yml
kubectl get services
kubectl describe svc echo-service-api
minikube service echo-service-api --url
> for IBM Cloud delivery pipeline need `deployment.yml`



## start
```
minikube start --vm-driver=hyperkit
kubectl version
kubectl get nodes
>NAME       STATUS   ROLES    AGE    VERSION
>minikube   Ready    master   2m9s   v1.18.0
eval $(minikube docker-env)

# build local machine and run test local
docker build --no-cache -t echo-service-with-mongo:v1 .
docker run -ti -p 3000:3000 echo-service-with-mongo:v1

kubectl get deploy
kubectl apply -f deployment.yml
kubectl get service -n swp
kubectl get deployment -n swp
kubectl get configmap -n swp
```




## Example deployment.yml
Separate using `---` 
```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: echo-service
  name: echo-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: echo-service
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: echo-service
    spec:
      containers:
      - image: echo-service
        name: echo-service
        imagePullPolicy: Never
        resources: {}
        ports:
          - containerPort: 3000
status: {}
---
apiVersion: v1
kind: Service
metadata:
  name: echo-service-api
spec:
  selector:
    app: echo-service
  ports:
  - protocol: TCP
    port: 3000
    targetPort: 3000
  type: LoadBalancer
```


