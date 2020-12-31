
## ubuntu lxc template

apt-get install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable" 

apt-get update

apt install docker-ce=17.09.1~ce-0~ubuntu

## minkube
apt-get install curl wget apt-transport-https -y

apt-get install conntrack

curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube

sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/
minikube version 

## minikube driver=none
systemctl enable kubelet.service

## minikube container runtime
VERSION="1.19"
OS="xUbuntu_18.04"
echo $VERSION
echo $OS
echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/ /" > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
echo "deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/$VERSION/$OS/ /" > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:cri-o:$VERSION.list

curl -L https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$VERSION/$OS/Release.key | apt-key add -
curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/Release.key | apt-key add -

apt-get update
apt-get install cri-o cri-o-runc

## kubectl
sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubectl
kubectl version --client

## user
adduser cg2p
usermod -a -G sudo cg2p

as cg2p:
sudo usermod -aG docker $USER && newgrp docker


## docker config
/etc/default/docker
DOCKER_OPTS="--exec-driver=lxc"

Exiting due to GUEST_PROVISION: Failed to start host: recreate: creating host: create: creating: create kic node: create container: docker run -d -t --privileged --security-opt seccomp=unconfined --tmpfs /tmp --tmpfs /run -v /lib/modules:/lib/modules:ro --hostname minikube --name minikube --label created_by.minikube.sigs.k8s.io=true --label name.minikube.sigs.k8s.io=minikube --label role.minikube.sigs.k8s.io= --label mode.minikube.sigs.k8s.io=minikube --volume minikube:/var --security-opt apparmor=unconfined --cpus=2 --memory=2199023206400mb --memory-swap=2199023206400mb -e container=docker --expose 8443 --publish=127.0.0.1::8443 --publish=127.0.0.1::22 --publish=127.0.0.1::2376 --publish=127.0.0.1::5000 gcr.io/k8s-minikube/kicbase:v0.0.12-snapshot3@sha256:1d687ba53e19dbe5fafe4cc18aa07f269ecc4b7b622f2251b5bf569ddb474e9b: exit status 125

