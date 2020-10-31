# Building And Installing A Kernel

## 1. Clone the stable kernel Git repo
```bash
$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git linux_stable
$ cd linux_stable/
$ git branch -a | grep linux-5
$ git checkout linux-5.9.y
```

## 2. Copy configuration of the current kernel as the configuration of thenew kernel as well
```bash
$ ls /boot
$ cp /boot/config-5.4.0-52-generic .config
```

## 3. Configure the kernel
There are 2 main steps to compile the kernel - Generate a kernel configuration file and compile the kernel.
### 3.1 Generate a kernel configuration
Generating a kernel configuration can happen in 2 ways - Use an existing configuration to create a new one (OR) create a configuration based on trimming down the kernel and tailoring to your system.
#### 3.1.1 Use an existing configuration to create a new one
```bash
$ make oldconfig
```
A series of steps will allow you to manually configure the kernel as needed.

### 3.1.2 Create a configuration based on trimming down the kernel and tailoring to your system.
```bash
$ lsmod> /tmp/my-lsmod
$ make LSMOD=/tmp/my-lsmod localmodconfig
```
A series of steps will allow you to manually configure the kernel as needed.

## 4. Compile the kernel
```bash
$ make -j3 all
```

## 5. Install the new kernel
```bash
$ su -c "make modules_install install"
```
This command installs the new kernel and adds it to the gub menu.

## 6. (OPTIONAL) Save logs from the current kernel to compare and look for regressions/new errors
```bash
$ dmesg -t > dmesg_current
$ dmesg -t -k > dmesg_kernel
$ dmesg -t -l emerg > dmesg_current_emerg
$ dmesg -t -l alert > dmesg_current_alert
$ dmesg -t -l crit > dmesg_current_crit
$ dmesg -t -l err > dmesg_current_err
$ dmesg -t -l warn > dmesg_current_warn
```

## 7. Reboot the system
### 7.1. Update */etc/default/grub* file to show the boot menu instead of booting the new kernel by default.
```bash
$ sudo vi /etc/default/grub
```

* Uncomment GRUB_TIMEOUT and set it to 10: GRUB_TIMEOUT=10
* Comment out GRUB_TIMEOUT_STYLE=hidden
* GRUB_CMDLINE_LINUX="earlyprink=vga"

```bash
$ sudo update-grub
$ sudo reboot now
```

