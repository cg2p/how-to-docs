# Minikube running in KVM VM on Antsle

## antlet Ubuntu 18.04 template
ssh ubuntu@10.1.1.11 / antsle
sudo <command>

```
sudo apt-get update
sudo apt-get dist-upgrade
cat /etc/os-release
# 18.04.5
```


## Nest KVM
Allow minikube KVM to run inside KVM antlet

https://linuxconfig.org/install-and-set-up-kvm-on-ubuntu-18-04-bionic-beaver-linux 

with sudo
```
# check non-emp
grep -E --color 'vmx|svm' /proc/cpuinfo
> empty

sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virt-manager

# setup network bridge so that VMs can access the KVM antlet's networking
ip a
> lo ens3 virbr0 virbr0-nic
```
vi /etc/network/interface 
```
auto lo br0
iface lo inet loopback

iface ens3 inet manual

iface br0 inet dhcp
    bridge_ports ens3

``` 
user can manage virtual machines
```
sudo adduser ubuntu libvirt
sudo adduser ubuntu libvirt-qemu
```

Nested:
```
cat /sys/module/kvm_intel/parameters/nested 
> Y

#if N
echo 'options kvm_intel nested=1' >> /etc/modprobe.d/qemu-system-x86.conf 

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


* Kubernetes 1.19 is out! Get it in one command with:

     sudo snap install microk8s --channel=1.19 --classic

   https://microk8s.io/ has docs and details.

   https://computingforgeeks.com/how-to-setup-openshift-origin-on-ubuntu/ 