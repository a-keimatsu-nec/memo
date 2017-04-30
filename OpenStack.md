# Openstack
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
