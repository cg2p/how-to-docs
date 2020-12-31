# Red Hat Code Ready Containers

## base
CRC 1.15
- OpenShift Container platform 4.5.7
- OpenShift binary (`oc`) 4.5.7

VM
- 4 vCPUs
- 12 GB RAM
- CentOS 7.5+

antlet template
- cg2p-centos-7.8

## 
yum install sudo

## Nested Virt
https://www.cyberciti.biz/faq/how-to-install-kvm-on-centos-7-rhel-7-headless-server/ 
lscpu | grep Virtualization
yum install qemu-kvm libvirt libvirt-python libguestfs-tools virt-install
systemctl enable libvirtd
systemctl start libvirtd


centos 7 kvm template
```
grep -E '(vmx|svm)' /proc/cpuinfo
> no output
```

https://www.linuxtechi.com/install-kvm-hypervisor-on-centos-7-and-rhel-7/ 
```
yum install qemu-kvm qemu-img virt-manager libvirt libvirt-python libvirt-client virt-install virt-viewer bridge-utils
systemctl start libvirtd
systemctl enable libvirtd
lsmod | grep kvm

```

## KVM nested
https://stafwag.github.io/blog/blog/2018/06/04/nested-virtualization-in-kvm/ 

### in edgeLinux
modprobe kvm_intel nested=1

cat /sys/module/kvm_intel/parameters/nested
Y

vi /etc/modprobe.d/kvm_intel.conf
> options kvm_intel nested=1

### in VM

http://ronaldbradford.com/blog/are-you-running-kvm-or-qemu-launched-instances-2016-05-19/


## CRC
dowload crc
```
wget https://mirror.openshift.com/pub/openshift-v4/clients/crc/latest/crc-linux-amd64.tar.xz
```

unpack and ensure in path
```
tar -xvf crc-linux-amd64.tar.xz
mv crc-linux-1.15.0-amd64/crc bin
```

CRC pull secret
```
{"auths":{"cloud.openshift.com":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2plcmVteWNhaW5lMWNjdnl6ZHZ5ZzJzcmRxaXJtN3NqcWdoOW80OkQ2UFJSWDFSMEZIOE5FS0NKSzFXTVpXVlROR1pPRENJVE1ZUFdMUVkxVFZZNDFUQlAyWkpCQUFPNVY1R0gyVVc=","email":"jezcaine@gmail.com"},"quay.io":{"auth":"b3BlbnNoaWZ0LXJlbGVhc2UtZGV2K2plcmVteWNhaW5lMWNjdnl6ZHZ5ZzJzcmRxaXJtN3NqcWdoOW80OkQ2UFJSWDFSMEZIOE5FS0NKSzFXTVpXVlROR1pPRENJVE1ZUFdMUVkxVFZZNDFUQlAyWkpCQUFPNVY1R0gyVVc=","email":"jezcaine@gmail.com"},"registry.connect.redhat.com":{"auth":"NTI2NTI0NzV8dWhjLTFjQ1Z5WmRWWUcyU1JkcUlyTTdzSlFnSDlPNDpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSTJNV0V3WkdNeFpUUTVOV00wWlRsbFlXTm1PRFl5T0RCbFkyTTNaVGhoT0NKOS5Xd0VGYVZHOHRBMXA2XzdNWEFGSXdyeU11NENkMmdfZVJNaTRUM3hzOG00NmRRTVZ3MTNfWXpTUW9sdnpYMllBVWVPMDR1eVhydHRNd2Y2MHhLSllwbGdDWThGUnlzbzJMNkhhU2RxazgyZUFxd2lHellROURrQmJyNUU2RXp0akJOT2hUSnRMd2N2WmRzdmZ4NUVTNVcxZmFDWldRX3NvcHdIbDJYSXlVekFTeFBvOVdlVmxkZmxaTEZJZGtXMmhBSmZLd0E2SFd6Yk9MN0FKSUFtT2liUEViamtKcXE4ZFd1Q1J2U05IdGQzUW5pUXF6N1JEeWZnQkFwYmdhYTNLTjlQdjB5TXdXR1V0UUIwYkZlSDA3MDBYMjdhVTctWmttbUhfV2RVZ2FmMUYtUnZHNlpLaWtRUmpVV1htUlczSjNJV3hfNHhTRHI3NTUzWkg3djBUTmJHMXBzZDRiTkFSdnVvODczZ0ZEejIwbWFOSHh4YXEzdi1qY2VFUVRxdnJQeHBmbTR2cUcyWWRZY0tKakh3TjN6OVUzeG51ejYzT0ViV3Vyb05BTVJJTnhoOU1XX0VyLXNnc3BoUlRQY1MwNGhjNmFmaUZvSGNEX3dLVDZIYlliRlpGVDN4N0RSeEpGdFVzdEpmaDlMeWY5SF92V19xRmFXNENteW1YNlJiR3VtenFMM3djaEdycUdYeUhjMWhTcWxRckQyU0h1eUZOUHpocFBNcGlLcmFLYWV5UTBpX2JtQm9NeVNKRGRUOEFoMTViNGdYYm5CeHlBazRPRUFPejA5Nk5vQVd3em1DdG9MS2padFAydkdhVFJqOU9xc2E5TV9VUVZPS1FjZWJiQkhRdzhzVWxjMmpIVTdwNDFWeUt3b29HbWFiRXRLSjFOUXNOZFhRbFc1RQ==","email":"jezcaine@gmail.com"},"registry.redhat.io":{"auth":"NTI2NTI0NzV8dWhjLTFjQ1Z5WmRWWUcyU1JkcUlyTTdzSlFnSDlPNDpleUpoYkdjaU9pSlNVelV4TWlKOS5leUp6ZFdJaU9pSTJNV0V3WkdNeFpUUTVOV00wWlRsbFlXTm1PRFl5T0RCbFkyTTNaVGhoT0NKOS5Xd0VGYVZHOHRBMXA2XzdNWEFGSXdyeU11NENkMmdfZVJNaTRUM3hzOG00NmRRTVZ3MTNfWXpTUW9sdnpYMllBVWVPMDR1eVhydHRNd2Y2MHhLSllwbGdDWThGUnlzbzJMNkhhU2RxazgyZUFxd2lHellROURrQmJyNUU2RXp0akJOT2hUSnRMd2N2WmRzdmZ4NUVTNVcxZmFDWldRX3NvcHdIbDJYSXlVekFTeFBvOVdlVmxkZmxaTEZJZGtXMmhBSmZLd0E2SFd6Yk9MN0FKSUFtT2liUEViamtKcXE4ZFd1Q1J2U05IdGQzUW5pUXF6N1JEeWZnQkFwYmdhYTNLTjlQdjB5TXdXR1V0UUIwYkZlSDA3MDBYMjdhVTctWmttbUhfV2RVZ2FmMUYtUnZHNlpLaWtRUmpVV1htUlczSjNJV3hfNHhTRHI3NTUzWkg3djBUTmJHMXBzZDRiTkFSdnVvODczZ0ZEejIwbWFOSHh4YXEzdi1qY2VFUVRxdnJQeHBmbTR2cUcyWWRZY0tKakh3TjN6OVUzeG51ejYzT0ViV3Vyb05BTVJJTnhoOU1XX0VyLXNnc3BoUlRQY1MwNGhjNmFmaUZvSGNEX3dLVDZIYlliRlpGVDN4N0RSeEpGdFVzdEpmaDlMeWY5SF92V19xRmFXNENteW1YNlJiR3VtenFMM3djaEdycUdYeUhjMWhTcWxRckQyU0h1eUZOUHpocFBNcGlLcmFLYWV5UTBpX2JtQm9NeVNKRGRUOEFoMTViNGdYYm5CeHlBazRPRUFPejA5Nk5vQVd3em1DdG9MS2padFAydkdhVFJqOU9xc2E5TV9VUVZPS1FjZWJiQkhRdzhzVWxjMmpIVTdwNDFWeUt3b29HbWFiRXRLSjFOUXNOZFhRbFc1RQ==","email":"jezcaine@gmail.com"}}}
```


