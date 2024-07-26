# kvm-kali-setup

Bash script to assist with setting up a Kali Linux virtual machine under KVM.

This script allows one to set up a Kali Linux virtual machine on a remote Linux system from the command line.

For info on setting up KVM on the host machine, refer to the [Debian Wiki KVM page](https://wiki.debian.org/KVM).

In addition to what is recommended there, it is recommended to also install `ovmf`

ovmf allows UEFI booting


Here is what I usually use:
```bash
apt install --no-install-recommends qemu-system libvirt-clients libvirt-daemon-system ovmf
apt install --no-install-recommends virtinst libguestfs-tools
```
Don't forget:
```bash
usermod -aG libvirt <user>
```
and re-login or run `newgrp libvirt` as the user


## osinfo-db

It is recommended to update osinfo-db with the latest info.  This is done with:
```bash
git clone https://gitlab.com/libosinfo/osinfo-db.git
apt install gettext osinfo-db-tools
cd osinfo-db
make

# this runs osinfo-db-import to import the latest data
sudo make install
```

This will make sure that `debian12` (or any later versions) can be selected for the --os-variant `virt-install` switch.


## Usage

Edit the variables `machineName`, `isoImage`, `machineMemory`, `diskSize`, and `cpuNumber`.  `machineMemory` is the number of Gigabytes.  Recommended values are:

machineMemory=2
diskSize=40
cpuNumber=2

For the ISO image, it is recommended to use the [NetInstaller image of Kali](https://www.kali.org/get-kali/#kali-installer-images).


