# MicroK8s on Ubuntu KBM VM on Antsle

## antlet Ubuntu 18.04 template
ssh ubuntu@<ip> / antsle
sudo <command>

```
apt update
apt dist-upgrade
apt install snapd
cat /etc/os-release
# 18.04.5
```

## microk8s

Kubernetes 1.19 is out! Get it in one command with:
https://microk8s.io/ has docs and details.
```
snap install microk8s --channel=1.19 --classic
sudo usermod -a -G microk8s $USER
sudo chown -f -R $USER ~/.kube
su - $USER
```x`

setup user to use kubectl: 
add `alias kubectl='microk8s kubectl'` to `./.bash_aliases`

add ons:
`microk8s enable dns storage`

```
microk8s stop
microk8s start
```

## test kube deploy
```
kubectl create deployment hello-micro --image=k8s.gcr.io/echoserver:1.10
kubectl get pods
kubectl expose deployment hello-micro --type=LoadBalancer --port=8080
kubectl get services
kubectl describe service/hello-micro
```

kubectl delete deployment simple-node
kubectl delete service simple-node
kubectl create deployment simple-node --image=docker.io/cg2p/simple-node:red
kubectl get pods
kubectl expose deployment simple-node --type=LoadBalancer --port=3000
kubectl get services
q

## networking
`/etc/netplan/50-cloud-init.yaml`
```
network:
    ethernets:
        ens3:
          dhcp4: false
          addresses:
            - 192.168.1.201/24
           gateway4: 192.168.1.1
           nameservers:
           addresses:
            - 192.168.1.1
            - 8.8.8.8
    version: 2
```

