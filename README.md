# cheat-sheet

Mostly about linux commands and software development.

## LVM: Logical Volumen Management

pvdisplay: Show physical Volumne
vgdisplay: Show volume group
lvdisplay: Show logical volumen

LVM needed? Today you most likey use linux a virtual machine. In a VM (my opinion) it does not make much sense to use LVM. 

### Hypervisor increased size of /dev/sda ....

Hypervisor (VMWare Vsphere, KVM, ...) increased size of /dev/sda of your virtual machine. Your goal: make the space available in the fileystem.

You might want to increase the size of /dev/sda2. Use [growpart](http://manpages.ubuntu.com/manpages/precise/man1/growpart.1.html). You can use `fdisk`, too. But `growpart` is easier, since not interactive.

Reload the partition table with `partprobe`. 

If you use lvm:

 * You need to resize the physical volume: `pvresize /dev/sda2`
 * Increase the size of the logical volumen: `lvresize -l +100%FREE system/home`

Increase the size of the filesystem: `resize2fs /dev/mapper/system-home`

If you don't use LVM. Then `pvresize` and `lvresize` is not needed.

## Images

### Reducing image size

In the past I used `jpegoptim`, but this tool only reduced the file size, not the resolution.

I found a better solution [on StackOverflow](https://stackoverflow.com/questions/34522269/how-to-shrink-and-optimize-images).
This reduces the resolution and the file size, which results in images which are much more like the original.

```
# Resize image to no more than 1000px wide and keep output file size below 100kB
convert image.jpg -resize '1000x>' -define jpeg:extent=100KB result.jpg
```
