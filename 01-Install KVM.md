# Index
1. Install Ubuntu on the baremetal machine
2. Configure Ubuntu
3. Install KVM packages
4. Create the virtual machines
<br />


# 1. Install Ubuntu on the baremetal machine
Baremetal machine specification:
- CPU: Intel Core i7
- Memory: 16 GB
- SSD: 256 GB 
<br />

The ubuntu-24.04.1-desktop-amd64.iso image is used to install Ubuntu on the baremetal machine.
<br />
<br />
<br />


# 2. Configure Ubuntu
Install vim:\
``` $ sudo apt install vim ```

## 2.1. Networking
Install bridge-utils package. It is a set of tools for creating and managing bridge devices:\
``` $ sudo apt install -y bridge-utils ```
<br />

Add necessary networking configuration for netplan:
```
$ sudo vi /etc/netplan/01-netcfg.yaml
network:
  version: 2
  ethernets:
    eno1:
      dhcp4: false
      dhcp6: false
  bridges:
    br0:
      interfaces:
        - eno1
      dhcp4: false
      dhcp6: false
      addresses:
        - 10.0.0.100/24
      routes:
        - to: default
          via: 10.0.0.1
      nameservers:
        addresses: [8.8.8.8]
      parameters:
        stp: false
```

``` 
$ sudo chmod 600 /etc/netplan/01-netcfg.yaml
$ sudo netplan apply
```

``` $ ip addr show ```
<br />
<img width="797" alt="image" src="https://github.com/user-attachments/assets/8d8def45-f487-4c84-a364-aec62a76a931">


## 2.2. Enable SSH
Install OpenSSH Server:\
``` $ sudo apt install openssh-server ```
<br />


## 2.3. Enable Remote Login
![image](https://github.com/user-attachments/assets/773e5e66-cfe2-40ee-8808-2c1e6efd8185)
<br />

![image](https://github.com/user-attachments/assets/517fdf96-b4c7-4df3-84bf-8621dbd4c700)
<br />
<br />
<br />


# 3. Install KVM packages
update Ubuntu:\
``` $ sudo apt update ```   

Check if virtualization is enabled:\
``` $ egrep -c '(vmx|svm)' /proc/cpuinfo ```
<br />
<img width="360" alt="image" src="https://github.com/user-attachments/assets/e903e274-cbc1-4560-a475-ed9517d1993e">

``` $ sudo apt install -y cpu-checker ```
<br />
``` $ kvm-ok ```
<br />
<img width="208" alt="image" src="https://github.com/user-attachments/assets/109df41f-07b5-48cb-9852-0100563cb3ed">

Install KVM packages:\
``` $ sudo apt install -y qemu-kvm virt-manager libvirt-daemon-system virtinst libvirt-clients ```
<br />
<br />

- **qemu-kvm:** An opensource emulator and virtualization package that provides hardware emulation.
- **virt-manager:** A Qt-based graphical interface for managing virtual machines via the libvirt daemon.
- **libvirt-daemon-system:** A package that provides configuration files required to run the libvirt daemon.
- **virtinst:** A  set of command-line utilities for provisioning and modifying virtual machines.
- **libvirt-clients:** A set of client-side libraries and APIs for managing and controlling virtual machines & hypervisors from the command line.
<br />
<br />

Start and enable the daemon:
```
$ sudo systemctl enable --now libvirtd
$ sudo systemctl start libvirtd
$ sudo systemctl status libvirtd
```
<br />
<br />

Add the current logged in user to kvm and libvirt groups:
```
$ sudo usermod -aG kvm $USER
$ sudo usermod -aG libvirt $USER
```

Reboot the system:\
``` $ sudo reboot ```
<br />
<br />

# 4. Create the virtual machines
Use Virtual Machine Manager tool to deploy the VMs needed:
<img width="1323" alt="image" src="https://github.com/user-attachments/assets/24328bb0-f82d-481c-9dd4-6f4c96369569">


Create 3 virtual machines as below if you haven't already:
- OS: debian-12.7.0-amd64-netinst.iso
- vCPU: 4
- Memory 4 GB
- Disk: 40 GB
<br />


![image](https://github.com/tachyon888/K8s-on-OpenStack-on-KVM/blob/main/images/02-01.jpg)
![image](https://github.com/tachyon888/K8s-on-OpenStack-on-KVM/blob/main/images/02-02.jpg)

<br />

Configure each VM:
- vm0: 10.0.0.110/24
- vm1: 10.0.0.111/24
- vm2: 10.0.0.112/24
<br />

```
# apt install vim

# vi /etc/network/interfaces
auto enp1s0
iface enp1s0 inet static
address 10.0.0.110
netmask 255.255.255.0
gateway 10.0.0.1
```
``` # systemctl restart networking ```
