# Minikube using Docker on CentOS KVM

## Base CentOS
- centios 7 kvm
- upgrade latest
+ cg2p
+ kubectl
+ minikube
+ crc

### Networking
- add br0 bridge
- reboot antlet

eth1 from docs.antlse

### upgrade to latest CentOS
upgrade to latest version OS
```
cat /etc/centos-release
> CentOS Linux release 7.2.1511 (Core) 

yum check-update
yum upgrade
yum install wget
yum install java // jdk 1.1.8
yum install sudo
```
### add in user
add in user
```
adduser cg2p
passwd cg2p
usermod -aG wheel cg2p
# add to sudoers files
visudo
> cg2p  ALL=(ALL) NOPASSWD:ALL
```
- Template it (eg. centos-kvm)

## Docker 

### Docker install
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

yum install -y yum-utils
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

yum install docker-ce docker-ce-cli containerd.io
yum list docker-ce --showduplicates | sort -r
systemctl start docker

sudo usermod -aG docker ${USER}

docker run hello-world

### autostart
sudo systemctl enable docker


## Reconfigure filesystem for Docker

### overlay2
https://bitraboy.wordpress.com/2018/03/14/docker-on-centos-overlay-storage/ 

```
systemctl stop docker
cp -au /var/lib/docker /var/lib/docker.bk
```

create virtual drive e.g. vdb and reboot antlet to see it at /dev/vdb

```
mkfs -t xfs -n ftype=1 /dev/vdb
vi /etc/fstab
# /dev/vdb /var/lib/docker xfs defaults 0 0 
mount -a
cp -au /var/lib/docker.bk/* /var/lib/docker
systemctl start docker
```

###  Set up the Docker daemon
```
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
sudo systemctl daemon-reload
sudo systemctl restart docker
```


## minikube
kubectl
```
sudo curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
sudo chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version --client
# GitVersion:"v1.19.2"
```

minikube
```
sudo curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && sudo chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/
```








