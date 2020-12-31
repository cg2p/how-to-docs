# minikube-docker

centos - LXC template

## docker
as root
```
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

# setup repo
yum install -y yum-utils
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo


# 1. install docker engine
yum install docker


https://stanislas.blog/2018/02/lxc-zfs-pool-lxd/ 
https://www.reddit.com/r/Proxmox/comments/a3g3af/53_docker_on_lxc_on_zfs/ 
https://openzfs.github.io/openzfs-docs/Getting%20Started/RHEL%20and%20CentOS.html 

# 2. zfs
# epel repo provides dkms
yum install epel-release
# dkms needs kernel-devel to build zfs
yum install "kernel-devel-uname-r == $(uname -r)" zfs


# 3. configure docker to use zfs https://docs.docker.com/storage/storagedriver/zfs-driver/ 
# zfs storage driver
cp -au /var/lib/docker /var/lib/docker.bk
rm -rf /var/lib/docker/*
> rm: cannot remove ‘/var/lib/docker/containers’: Device or resource busy

udevadm trigger
mount -t proc proc /proc
zpool create -f zpool-docker -m /var/lib/docker /dev/xvdf /dev/xvdg
zfs list

vi /etc/docker/daemon.json
{  
 "storage-driver": "zfs"
}

cp /etc/sysconfig/docker-storage /etc/sysconfig/docker-storage.bk
vi /etc/sysconfig/docker-storage
> DOCKER_STORAGE_OPTIONS="--storage-driver zfs "

***???***

systemctl start docker
docker info
docker run hello-world


```
## minikube-podman-crio
https://computingforgeeks.com/install-cri-o-container-runtime-on-centos-linux/
https://minikube.sigs.k8s.io/docs/handbook/config/ 
https://minikube.sigs.k8s.io/docs/drivers/podman/ 


## minikube
minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && sudo chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/

yum install conntrack
sudo usermod --append --groups libvirt `whoami`

minikube start --driver=kvm2
```

## debuggin

yum install setroubleshoot setools
yum remove setroubleshoot setools


