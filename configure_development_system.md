# Configure Your Development System

Follow these steps to configure your development system to compile Linux kernels.

## 1. Install a Linux distribution in your development system
Install one of the popular Linux distributions or a Linux VM. I used a Ubuntu 20.10 VM installed on my Linux Box for the purpose of this porject. Here are the brief steps I used to setup a working Linux environment.

### 1.1 Install KVM on the Host OS
Refer instructions in [install_kvm.md]

### 1.2 Install Ubuntu 20.10 using QEMU-KVM on the Host OS
Refer instructions in [install_kvm.md]

## 2. Set aside at least 3gb disk space for the boot partition in your development system
## 3. Enable the root account
## 4. Enable sudo for your account
## 5. Install essential packages to build linux kernels
```bash
$ sudo apt install -y build-essential vim git cscope libncurses-dev libssl-dev bison flex
$ sudo apt install -y git-email
```

##References:
1. https://www.kernel.org/doc/html/latest/process/changes.html
2. https://trainingportal.linuxfoundation.org/learn/course/a-beginners-guide-to-linux-kernel-development-lfd103/configuring-your-development-system/configuring-your-development-system
