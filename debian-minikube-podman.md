# Debian 10

## podman
https://minikube.sigs.k8s.io/docs/drivers/podman/

echo 'deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/Debian_10/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list

curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/Debian_10/Release.key | sudo apt-key add -

sudo apt-get update -qq
sudo apt-get -qq -y install podman




## docker
repository
```
apt-get remove docker docker-engine docker.io containerd runc
apt-get update
apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
apt-key fingerprint 0EBFCD88
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
```

docker engine
```
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io
docker run hello-world
```

as $USER
```
sudo groupadd docker
sudo usermod -aG docker $USER
```
restart
```
docker run hello-world
```

## minikube
ubectl
```
sudo curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
sudo chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version --client
# GitVersion:"v1.19.2"
```

minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && sudo chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/
```


## overlay2
https://bitraboy.wordpress.com/2018/03/14/docker-on-centos-overlay-storage/ 

create virtual drive e.g. vdb and reboot antlet to see it at /dev/vdb

systemctl stop docker
cp -au /var/lib/docker /var/lib/docker.bk
umount /dev/vda1



## Set up the Docker daemon
cat <<EOF | sudo tee /etc/docker/daemon.json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
sudo mkdir -p /etc/systemd/system/docker.service.d
# Restart Docker
    sudo systemctl daemon-reload
    sudo systemctl restart docker

systemctl enable kubelet.service
```
apt-get install conntrack
minikube start --driver=none
```


