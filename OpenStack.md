# OpenStack
## Initialize
* Machine Spec of Main Controller
  * RAM: Over 8GB
  * CPU: Over 2CPU
  * OS: CentOS 7.X

1. Install CentOS
2. Disable firewalld, NetworkManager
```
systemctl disable firewalld
systemctl stop firewalld
systemctl disable NetworkManager
systemctl stop NetworkManager
```
3. Disable SELinux
```
setenforce 0
vi /etc/selinux/config
```
4. Install RDO
```
yum install -y centos-release-openstack-ocata
yum update -y
yum install -y openstack-packstack
packstack --allinone --keystone-admin-passwd=<adminpasswd>
```
5. Browse ```http://<HOST>/```

## Add Compute Node
1. Edit answer-file
```
vi ~/packstack-answers-YYYYMMDD-hhmmss.txt
CONFIG_COMPUTE_HOSTS=<serverIP>,<serverIP>,...
EXCLUDE_SERVERS=<already-configured-serverIP>,...
```
2. Apply
```
packstack --answer-file=~/packstack-answers-YYYYMMDD-hhmmss.txt
```

## If install fails...
* Check log files
  * `/var/tmp/packstack/latest/openstack-setup.log`
  * `/var/tmp/packstack/<hashID?>/manifests/<Host>_compute.pp.running`
* If the error "network is unreachable" shows in Glance installation"...
  * Glance needs internet access to get cirros image. Glance installation fails using proxy, and I don't know how to set proxy for getting cirros image. So, build web server and put images ( pre-downloaded manually ).
  * Set below options when packstack executes.
```
--provision-image-url=http://SERVER/path/to/cirros-0.3.4-x86_64-disk.img --provision-uec-kernel-url=http://SERVER/path/to/cirros-0.3.4-x86_64-kernel --provision-uec-ramdisk-url=http://SERVER/path/to/cirros-0.3.4-x86_64-initramfs --provision-uec-disk-url=http://SERVER/path/to/cirros-0.3.4-x86_64-disk.img
```
