# Templates
Antlet templates for cg2p environment



cg2p-debian-9-lxx
cg2p-debian-10-lxc
minikube


TODO
- take v9 and do installs, new v9
- upg v9 to v10 and new v10 temp
- minikube derived from cg2p-debian-10-lxc

## Debian or Ubuntu installs
- curl
- python

- Java

### curl
apt-get install curl

### python
apt-get install python

### java headless (no gui libs)
apt-get install openjdk-8-jdk-headless



### docker
```
apt-get update

apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
apt-key fingerprint 0EBFCD88

# chipset
uname -a

add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

apt-get update
apt-get install docker-ce docker-ce-cli containerd.io

docker run hello-world
```

### minikube
check non-empty output
```
grep -E --color 'vmx|svm' /proc/cpuinfo
```

kubectl
```
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version --client
```

podman
```
echo 'deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/Debian_10/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/Debian_10/Release.key | sudo apt-key add -

sudo apt update
sudo apt -y install podman

# add to /etc/sudoers by using `sudo visudo`
# cg2p ALL=(ALL) NOPASSWD: /usr/bin/podman
```

docker
```
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo docker run hello-world
sudo usermod -aG docker $USER && newgrp docker

minikube start --driver=docker
```

kvm2
```
sudo apt-get install libvirt-clients libvirt-daemon-system qemu-kvm
sudo usermod -aG libvirt $(whoami)
newgrp libvirt
curl -LO https://storage.googleapis.com/minikube/releases/latest/docker-machine-driver-kvm2 \
  && sudo install docker-machine-driver-kvm2 /usr/local/bin/
minikube start --driver=kvm2
```

minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/

yum install conntrack
apt-get install conntrack

minikube start --driver=podman
```

```

## java
apt install openjdk-8-jdk