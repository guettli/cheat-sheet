# cheat-sheet

Mostly about linux commands and software development.

## LVM: Logical Volumen Management

pvdisplay: Show physical Volumne
vgdisplay: Show volume group
lvdisplay: Show logical volumen

LVM needed? Today you most likey use linux a virtual machine. In a VM (my opinion) it does not make much sense to use LVM. 

### Hypervisor increased size of /dev/sda ....

Hypervisor (VMWare Vsphere, KVM, ...) increased size of /dev/sda of your virtual machine.

You might want to increase the size of /dev/sda2. Use [growpart](http://manpages.ubuntu.com/manpages/precise/man1/growpart.1.html). You can use `fdisk`, too. But `growpart` is easier, since not interactive.

Reload the partition table with `partprobe`.

You need to resize the physical volume: `pvresize /dev/sda2`

Increase the size of the logical volumen: `lvresize -l +100%FREE system/home`

Increase the size of the filesystem: `resize2fs /dev/mapper/system-home`

