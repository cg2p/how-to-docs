https://access.redhat.com/solutions/64069 

```
yum install screen
yum history
yum history undo 17
yum history undo 17
package-cleanup --orphans
package-cleanup --problems
package-cleanup --dupes
package-cleanup --leaves

```

Loaded plugins: fastestmirror, langpacks
ID     | Login user               | Date and time    | Action(s)      | Altered
-------------------------------------------------------------------------------
    18 | root <root>              | 2020-09-14 03:26 | Install        |    1   
    17 | root <root>              | 2020-09-08 04:11 | I, U           |   48   
    16 | root <root>              | 2020-09-07 03:47 | I, U           |  128 EE
    15 | System <unset>           | 2020-06-12 14:06 | Install        |    1   
    14 | System <unset>           | 2020-06-12 14:03 | Install        |  152   
    13 | System <unset>           | 2020-06-12 14:02 | Install        |   10   
    12 | System <unset>           | 2020-06-12 13:54 | Install        |    8   
    11 | System <unset>           | 2020-06-12 13:53 | Install        |    1   
    10 | System <unset>           | 2020-06-12 13:53 | I, U           |   15   
     9 | System <unset>           | 2020-06-12 13:52 | Install        |  195   
     8 | System <unset>           | 2020-06-12 13:52 | Install        |    1   
     7 | System <unset>           | 2020-06-12 13:52 | Update         |    1   
     6 | System <unset>           | 2020-06-12 13:51 | Install        |    4   
     5 | System <unset>           | 2020-06-12 13:43 | Install        |   23   
     4 | System <unset>           | 2020-06-12 13:42 | Install        |    1   
     3 | System <unset>           | 2020-06-12 13:40 | O, U           |  134 EE
     2 | System <unset>           | 2020-06-12 13:39 | Install        |    2   
     1 | System <unset>           | 2020-05-21 11:07 | Install        |  301 

yum install dkms


yum erase zfs zfs-dkms libzfs2 spl spl-dkms libzpool2 -y
reboot
yum install zfs -y



yum list kernel --show-duplicates

insmod /lib/modules/3.10.0-1062.9.1.el7.x86_64/extra/zfs/zfs/zfs.ko

https://openzfs.github.io/openzfs-docs/Getting%20Started/RHEL%20and%20CentOS.html

cat /etc/centos-release
uname -r
rpm -qa | grep zfs
rpm -q kmod-zfs -l

> centos 7.8
yum install http://download.zfsonlinux.org/epel/zfs-release.el7_8.noarch.rpm
gpg --quiet --with-fingerprint /etc/pki/rpm-gpg/RPM-GPG-KEY-zfsonlinux



yum remove zfs zfs-kmod spl spl-kmod libzfs2 libnvpair1 libuutil1 libzpool2 zfs-release
yum install http://download.zfsonlinux.org/epel/zfs-release.el7_8.noarch.rpm
yum autoremove
yum clean metadata
yum install zfs
/sbin/modprobe zfs

yum install epel-release
yum install "kernel-devel-uname-r == $(uname -r)" zfs

/sbin/modprobe zfs
zpool import -a

> docker start probkems
cp -au /var/lib/docker /var/lib/docker.bk
rm -rf /var/lib/docker/*
zpool create -f zpool-docker -m /var/lib/docker /dev/xvdf /dev/xvdg
