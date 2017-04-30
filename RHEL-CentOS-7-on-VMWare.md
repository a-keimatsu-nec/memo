1. Generate VM with CentOS/RHEL ISO.
2. Boot
3. Install with network configuration and reboot.
4. Attach VMWareTools
5. ( If OS is RHEL, create local repository. )
6. Install dependent packages with VMWareTools.
```
yum -y install perl gcc net-tools
yum -y install kernel-devel-`uname -r`
```
7. Install VMWareTools.
```
mkdir /mnt/cdrom
mount /dev/cdrom /mnt/cdrom
cp /mnt/cdrom/VMWareTools-XXX.tar.gz /tmp/
cd /tmp
tar zxvf VMWareTools-XXX.tar.gz
cd vmware-tools-distrib
./vmware-install.pl
```

