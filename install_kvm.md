# Install KVM on Ubuntu 20.04 LTS

## 1. Prerequisites
### 1.1 Check virtualization support on Ubuntu

```bash
$ egrep -c '(vmx|svm)' /proc/cpuinfo
8
```
An output greater than 0 means that virtualization is supported.

### 1.2 Check if KVM virtualization is supported

```bash
$ sudo apt install cpu-checker
$ kvm-ok
INFO: /dev/kvm exists
KVM acceleration can be used
```
The output should indicate if KVM is supported or not.

## 2. Install KVM on Ubuntu 20.04

```bash
$ sudo apt install -y qemu qemu-kvm libvirt-daemon libvirt-clients bridge-utils virt-manager
```

## 3. Ensure that virtualization daemon is running (enable it if needed)

```bash
$ sudo systemctl status libvirtd
$ sudo systemctl enable --now libvirtd
$ lsmod | grep -i kvm
```
## 5. Logout and log back in

## 6. Create a VM using GUI

```bash
$ virt-manager
```

Or you can also open this from the Ubuntu Dash. CLick on the "Show Applications" icon in the desktop and type "virtual machine manager" in the search bar.

## 7. (OPTIONAL) Create a VM using CLI

```bash
$ sudo virt-install --name=deepin-vm --os-variant=Debian10 --vcpu=2 --ram=2048 --graphics spice --location=/home/Downloads/deepin-20Beta-desktop-amd64.iso --network bridge:vibr0 
```

References: 
1. https://www.tecmint.com/install-kvm-on-ubuntu/
2. https://www.cyberciti.biz/faq/how-to-install-kvm-on-ubuntu-20-04-lts-headless-server
3. https://askubuntu.com/questions/345218/virt-manager-cant-connect-to-libvirt/345263#345263?newreg=dd6b759e87c94768bcae67bf0ffdbf81
4. https://linuxhint.com/install_kvm_ubuntu-2/
