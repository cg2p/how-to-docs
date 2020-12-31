# Antsle Virtualisation Architecture


- "L0" – the bare metal host, running KVM
- "L1" – a VM running on L0; also called the "guest hypervisor" — as it itself is capable of running KVM
- "L2" – a VM running on L1, also called the "nested guest"

Running edgeLinux = custom centOS 7.8 and enable for nesting
```
# cat /etc/modprobe.d/kvm_intel.conf
options kvm_intel nested=1
```

## Install KVM on L1
https://ostechnix.com/how-to-enable-nested-virtualization-in-kvm-in-linux/ 
```
lscpu | grep Virtualization

yum install -y qemu-kvm qemu-img virt-manager libvirt libvirt-python libvirt-client virt-install virt-viewer

virt-host-validate

systemctl start libvirtd
systemctl enable libvirtd
lsmod | grep kvm
```

Create L2 VM from template 'CentOS-7 KVM'
Ensure VM are stopped


edit the L2 guest KVM VM
```
virsh list --all
virsh edit cent-kvm

> change cpu mode to host-model
> <cpu mode='host-model' check='partial'/>

start cent-kvm
virsh list --all

dumpxml cent-kvm
```

https://linuxconfig.org/how-to-create-and-manage-kvm-virtual-machines-from-cli

## Check nested KVM on L2 is enabled
```
virt-host-validate
> QEMU: Checking for hardware virtualization                                 : PASS
> QEMU: Checking if device /dev/kvm exists                                   : PASS
```

# Upgrade VM and Template
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

add in user
```
adduser cg2p
passwd cg2p
usermod -aG wheel cg2p
# add to sudoers files
visudo
> cg2p  ALL=(ALL) NOPASSWD:ALL
```
template it

# minikube
minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/

yum install conntrack
sudo usermod --append --groups libvirt `whoami`

minikube start --driver=kvm2
```

# kubectl
```
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version --client
```

# edgeLinux Virutalisation topics
[create antlet lxc and kvm from cli](https://edgelinux.org/forum/topic/tutorial-on-creating-an-antlet-from-the-cli-nice-to-have/)

LXC
https://serverfault.com/questions/366575/is-it-possible-to-start-lxc-container-inside-lxc-container
https://stgraber.org/2013/12/21/lxc-1-0-advanced-container-usage/


# network
https://help.ubuntu.com/community/KVM/Networking 

```
ssh root@10.1.1.nn
ip addr
> see eth1 on 192
  3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
      link/ether 52:54:00:52:a1:c2 brd ff:ff:ff:ff:ff:ff
      inet 192.168.1.15/24 brd 192.168.1.255 scope global noprefixroute dynamic eth1
        valid_lft 86364sec preferred_lft 86364sec
      inet6 fe80::9fa4:af73:d28e:bdc/64 scope link noprefixroute 
        valid_lft forever preferred_lft forever
```

vi /etc/sysconfig/network-scripts/ifcfg-eth1
```
add:
```
TYPE="Ethernet"
DEVICE="eth1"

ONBOOT="yes"
IPV4_FAILURE_FATAL="no"

BOOTPROTO="none"
IPADDR="192.168.1.10"
PREFIX="24"
GATEWAY="192.168.1.1"
DEFROUTE="yes"
DNS1="8.8.8.8"

-- dhcp

TYPE="Ethernet"
DEVICE="eth1"
ONBOOT="yes"
IPV4_FAILURE_FATAL="no"
BOOTPROTO="dhcp"
GATEWAY="192.168.1.1"
DEFROUTE="yes"
```
then restart
```
systemctl restart network

```
kubectl delete services hello-minikube
kubectl delete deployment hello-minikube
kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10
kubectl expose deployment hello-minikube --type=NodePort --port=8080 
minikube service hello-minikube --url

kubectl expose deployment hello-minikube --type=LoadBalancer --port=8080

kubectl expose deployment hello-minikube --type=NodePort --port=8080 
kubectl expose deployment hello-minikube --external-ip=192.168.1.15 --type=NodePort --port=8080

kubectl get pod
  minikube service hello-minikube --url

kubectl expose deployment hello-minikube --type=NodePort --port=8080 --target-port=8080

kubectl get svc/hello-minikube -n kube-system -o jsonpath='{.spec.ports[0].nodePort}'
```

# antsle
wget -c https://static-files.hau.to:8443/edgeLinux/edgelinux-rollback.sh
chmod +x edgelinux-rollback.sh
./edgelinux-rollback.sh