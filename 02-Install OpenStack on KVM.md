# Index
1. Create virtual machines
2. Install OpenStack

# 1. Create virtual machines
Create 3 virtual machines as below if you haven't already:
- OS: debian-12.7.0-amd64-netinst.iso
- vCPU: 4
- Memory 4 GB
- Disk: 40 GB
<br />


![image](https://github.com/tachyon888/K8s-on-OpenStack-on-KVM/blob/main/images/02-01.jpg)
![image](https://github.com/tachyon888/K8s-on-OpenStack-on-KVM/blob/main/images/02-02.jpg)

<br />

## Configure each VM:
vm0: 10.0.0.110/24 \
vm1: 10.0.0.111/24 \
vm2: 10.0.0.112/24

``` $ sudo apt install vim ```
```
$ sudo vi /etc/network/interfaces
auto enp1s0
iface enp1s0 inet static
address 10.0.0.110
netmask 255.255.255.0
gateway 10.0.0.1
```
``` $ sudo systemctl restart networking ```
