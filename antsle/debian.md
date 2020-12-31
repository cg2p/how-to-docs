# Debian 10 build

## Antlet
- Create from 'debian - lxc' template
- 2 vCPU, 2GB RAM, inherit compression

ssh root@myantsle 
ssh root@10.1.1.12
ssh -p 22012 cg2p@192.168.1.9

Add in a user
```
adduser cg2p
apt-get update
apt-get install sudo

# as root
usermod -a -G sudo cg2p
```

## Upgrade to latest Debian 8
Upgrade latest version
```
# update debian
apt update
apt upgrade
apt-get dist-upgrade
apt install nano

# when both below return null, then can upgrade to 9
dpkg --audit
dpkg --get-selections | grep hold
```
## Upgrade Debian 8 to 9
```
nano /etc/apt/sources.list

# replace contents with
deb http://httpredir.debian.org/debian stretch main contrib non-free
deb http://httpredir.debian.org/debian stretch-updates main contrib non-free
deb http://security.debian.org stretch/updates main contrib non-free

apt-get update
apt list --upgradable
apt-get upgrade
apt-get dist-upgrade
reboot
```
check version 9
```
cat /etc/os-release
cat /etc/debian_version
```

## Upgrade Debian 9 to 10
```
vi /etc/apt/sources.list

# replace to  
deb http://httpredir.debian.org/debian buster main
deb http://httpredir.debian.org/debian buster-updates main
deb http://security.debian.org buster/updates main

apt-get update
apt-get upgrade
apt-get dist-upgrade
reboot
```
## Networking
Configure a virtual nic
https://docs.antsle.com/networking/bridge#configure-virtual-nic 
which appears on br0
```
ip addr show

vi  
# add to top
auto eth1
iface eth1 inet dhcp

# restart network service
ifup eth1

# assigns a 192. address
```

## xfs


create virtual drive e.g. vda and boot VM
```
apt-get install xfsprogs
mkfs.xfs /dev/vda
```

## docker


## docker filesystem


##  Set up the Docker daemon
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

vi /etc/fstab
> /dev/vdb /var/lib/docker xfs defaults 0 0 
mount -a
cp -au /var/lib/docker.bk/* /var/lib/docker
systemctl start docker


```
systemctl stop docker
cp -au /var/lib/docker /var/lib/docker.bk
```