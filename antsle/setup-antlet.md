# Antlet

## Bridge NIC
antlet10 - 10.1.1.12 / 192.168.1.12

https://docs.antsle.com/networking/bridge#centos

```
ssh root@10.1.1.12
ip addr

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
```
then restart
```
systemctl restart network
```

## Upgrade CentOS 7 to 8
```
yum update -y
yum install -y epel-release
yum install -y yum-utils rpmconf
rpmconf -a # option 'N'
package-cleanup --leaves
package-cleanup --orphans
yum install -y dnf
dnf -y remove yum yum-metadata-parser
rm -Rf /etc/yum
dnf upgrade -y
dnf install http://mirror.centos.org/centos/8/BaseOS/x86_64/os/Packages/centos-release-8.2-2.2004.0.1.el8.x86_64.rpm
```

## Upgrade CentOS 7.x to 7.6
```
cat /etc/redhat-release
yum check-update
```

## CentOs 7.1

```
    yum install wget
wget --version
wget https://mirror.openshift.com/pub/openshift-v4/clients/crc/latest/crc-linux-amd64.tar.xz
mv mv crc-linux-amd64.tar.xz /usr/local/sbin
yum install xz
xz -d -v crc-linux-amd64.tar.xz
yum install tar
tar -xvf crc-linux-amd64.tar.xz
# copy pull secret
crc setup
```

{"auths":{"cloud.openshift.com":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2plcmVteWNhaW5lMWNjdnl6ZHZ5ZzJzcmRxaXJtN3NqcWdoOW80OkQ2UFJSWDFSMEZIOE5FS0NKSzFXTVpXVlROR1pPRENJVE1ZUFdMUVkxVFZZNDFUQlAyWkpCQUFPNVY1R0gyVVc=","email":"jezcaine@gmail.com"},"quay.io":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2plcmVteWNhaW5lMWNjdnl6ZHZ5ZzJzcmRxaXJtN3NqcWdoOW80OkQ2UFJSWDFSMEZIOE5FS0NKSzFXTVpXVlROR1pPRENJVE1ZUFdMUVkxVFZZNDFUQlAyWkpCQUFPNVY1R0gyVVc=","email":"jezcaine@gmail.com"},"registry.connect.redhat.com":{"auth":"NTI2NTI0NzV8dWhjLTFjQ1Z5WmRWWUcyU1JkcUlyTTdzSlFnSDlPNDpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSTJNV0V3WkdNeFpUUTVOV00wWlRsbFlXTm1PRFl5T0RCbFkyTTNaVGhoT0NKOS5Xd0VGYVZHOHRBMXA2XzdNWEFGSXdyeU11NENkMmdfZVJNaTRUM3hzOG00NmRRTVZ3MTNfWXpTUW9sdnpYMllBVWVPMDR1eVhydHRNd2Y2MHhLSllwbGdDWThGUnlzbzJMNkhhU2RxazgyZUFxd2lHellROURrQmJyNUU2RXp0akJOT2hUSnRMd2N2WmRzdmZ4NUVTNVcxZmFDWldRX3NvcHdIbDJYSXlVekFTeFBvOVdlVmxkZmxaTEZJZGtXMmhBSmZLd0E2SFd6Yk9MN0FKSUFtT2liUEViamtKcXE4ZFd1Q1J2U05IdGQzUW5pUXF6N1JEeWZnQkFwYmdhYTNLTjlQdjB5TXdXR1V0UUIwYkZlSDA3MDBYMjdhVTctWmttbUhfV2RVZ2FmMUYtUnZHNlpLaWtRUmpVV1htUlczSjNJV3hfNHhTRHI3NTUzWkg3djBUTmJHMXBzZDRiTkFSdnVvODczZ0ZEejIwbWFOSHh4YXEzdi1qY2VFUVRxdnJQeHBmbTR2cUcyWWRZY0tKakh3TjN6OVUzeG51ejYzT0ViV3Vyb05BTVJJTnhoOU1XX0VyLXNnc3BoUlRQY1MwNGhjNmFmaUZvSGNEX3dLVDZIYlliRlpGVDN4N0RSeEpGdFVzdEpmaDlMeWY5SF92V19xRmFXNENteW1YNlJiR3VtenFMM3djaEdycUdYeUhjMWhTcWxRckQyU0h1eUZOUHpocFBNcGlLcmFLYWV5UTBpX2JtQm9NeVNKRGRUOEFoMTViNGdYYm5CeHlBazRPRUFPejA5Nk5vQVd3em1DdG9MS2padFAydkdhVFJqOU9xc2E5TV9VUVZPS1FjZWJiQkhRdzhzVWxjMmpIVTdwNDFWeUt3b29HbWFiRXRLSjFOUXNOZFhRbFc1RQ==","email":"jezcaine@gmail.com"},"registry.redhat.io":{"auth":"NTI2NTI0NzV8dWhjLTFjQ1Z5WmRWWUcyU1JkcUlyTTdzSlFnSDlPNDpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSTJNV0V3WkdNeFpUUTVOV00wWlRsbFlXTm1PRFl5T0RCbFkyTTNaVGhoT0NKOS5Xd0VGYVZHOHRBMXA2XzdNWEFGSXdyeU11NENkMmdfZVJNaTRUM3hzOG00NmRRTVZ3MTNfWXpTUW9sdnpYMllBVWVPMDR1eVhydHRNd2Y2MHhLSllwbGdDWThGUnlzbzJMNkhhU2RxazgyZUFxd2lHellROURrQmJyNUU2RXp0akJOT2hUSnRMd2N2WmRzdmZ4NUVTNVcxZmFDWldRX3NvcHdIbDJYSXlVekFTeFBvOVdlVmxkZmxaTEZJZGtXMmhBSmZLd0E2SFd6Yk9MN0FKSUFtT2liUEViamtKcXE4ZFd1Q1J2U05IdGQzUW5pUXF6N1JEeWZnQkFwYmdhYTNLTjlQdjB5TXdXR1V0UUIwYkZlSDA3MDBYMjdhVTctWmttbUhfV2RVZ2FmMUYtUnZHNlpLaWtRUmpVV1htUlczSjNJV3hfNHhTRHI3NTUzWkg3djBUTmJHMXBzZDRiTkFSdnVvODczZ0ZEejIwbWFOSHh4YXEzdi1qY2VFUVRxdnJQeHBmbTR2cUcyWWRZY0tKakh3TjN6OVUzeG51ejYzT0ViV3Vyb05BTVJJTnhoOU1XX0VyLXNnc3BoUlRQY1MwNGhjNmFmaUZvSGNEX3dLVDZIYlliRlpGVDN4N0RSeEpGdFVzdEpmaDlMeWY5SF92V19xRmFXNENteW1YNlJiR3VtenFMM3djaEdycUdYeUhjMWhTcWxRckQyU0h1eUZOUHpocFBNcGlLcmFLYWV5UTBpX2JtQm9NeVNKRGRUOEFoMTViNGdYYm5CeHlBazRPRUFPejA5Nk5vQVd3em1DdG9MS2padFAydkdhVFJqOU9xc2E5TV9VUVZPS1FjZWJiQkhRdzhzVWxjMmpIVTdwNDFWeUt3b29HbWFiRXRLSjFOUXNOZFhRbFc1RQ==","email":"jezcaine@gmail.com"}}}


https://www.redhat.com/sysadmin/codeready-containers
```
su -c 'yum install NetworkManager'

mkdir /home/<user>/crc
wget https://mirror.openshift.com/pub/openshift-v4/clients/crc/latest/crc-linux-amd64.tar.xz
tar -xvf crc-linux-amd64.tar.xz

mv /home/cg2p/crc-linux-1.14.0-amd64/* /home/cg2p/crc
rm /home/cg2p/crc-linux-amd64.tar.xz
rm -r /home/cg2p/crc-linux-1.14.0-amd64

cd /home/cg2p/crc
chmod +x crc
export PATH=$PATH:/home/cg2p/crc

# as root: yum install sudo
# vi /etc/sudoers
#username  ALL=(ALL) NOPASSWD:ALL

crc setup
$ crc start -p /<path-to-the-pull-secret-file>/pull-secret.txt
```