# ubuntu

- base 18.04

## bridge
- add bridge network
- configure eth1 https://docs.antsle.com/networking/bridge#debianubuntu 

https://www.techrepublic.com/article/how-to-create-a-bridge-network-on-linux-with-netplan/ 
hostname

`hostnamectl set-hostname foobar`
vi /etc/hosts

## dns
apt update
apt dist-upgrade
apt install bind9
apt install dnsutils
vi /etc/bind/named.conf.options > add google 8.8.8.8
systemctl restart bind9







## minikube install
as root
```
apt-get install curl wget apt-transport-https -y

wget https://download.virtualbox.org/virtualbox/6.1.14/virtualbox-6.1_6.1.14-140239~Ubuntu~bionic_amd64.deb
apt install ./virtualbox-6.1_6.1.14-140239~Ubuntu~bionic_amd64.deb

This system is currently not set up to build kernel modules.
apt install virtualbox-guest-utils virtualbox-guest-dkms
apt install virtualbox-dkms

wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x /usr/local/bin/minikube
cp minikube-linux-amd64 /usr/local/bin/minikube
minikube version

```
apt-get install virtualbox virtualbox-ext-pack

sudo apt-get install virtualbox-dkms
sudo dpkg-reconfigure virtualbox-dkms 
sudo dpkg-reconfigure virtualbox

apt-get 
apt-get install virtualbox-dkms linux-headers-
WARNING: The character device /dev/vboxdrv does not exist.
	 Please install the virtualbox-dkms package and the appropriate
	 headers, most likely linux-headers-.

	 You will not be able to start VMs until this problem is fixed.


## kubectl
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | tee /etc/apt/sources.list.d/kubernetes.list
apt-get update -y
apt-get install kubectl -y
kubectl version -o json
```

## user permissions
```
adduser cg2p
passwd cg2p

# add to sudoers files
visudo
> cg2p  ALL=(ALL) NOPASSWD:ALL
```

## minikube start
as cg2p
```
minikube start
```
