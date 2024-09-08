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
## Enable SSH
## Enable Remote Login
## Configure Networking
<br />


# 3. Install KVM
update Ubuntu:
``` $ sudo apt update ```   

Check if virtualization is enabled:
``` $ egrep -c '(vmx|svm)' /proc/cpuinfo ```
<br />
<img width="360" alt="image" src="https://github.com/user-attachments/assets/e903e274-cbc1-4560-a475-ed9517d1993e">

``` $ sudo apt install -y cpu-checker ```
<br />
``` $ kvm-ok ```
<br />
<img width="208" alt="image" src="https://github.com/user-attachments/assets/109df41f-07b5-48cb-9852-0100563cb3ed">

