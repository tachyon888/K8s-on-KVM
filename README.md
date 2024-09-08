# Index
1. Install Ubuntu on the baremetal machine
2. Configure Ubuntu
3. Install KVM
4. Deploy Virtual Machines to install K8s cluster
5. Install K8s
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

# 2. Configure Ubuntu
## Configure Networking
Install bridge-utils package. It is a set of tools for creating and managing bridge devices.\
``` $ sudo apt install -y bridge-utils ```
<br />

## Enable SSH
Install OpenSSH Server:\
``` $ sudo apt install openssh-server ```
<br />

## Enable Remote Login
![image](https://github.com/user-attachments/assets/773e5e66-cfe2-40ee-8808-2c1e6efd8185)
<br />

![image](https://github.com/user-attachments/assets/517fdf96-b4c7-4df3-84bf-8621dbd4c700)
<br />



# 3. Install KVM
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

  
