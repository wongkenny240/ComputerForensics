# Mounting an image to a VM

## FTK Imager

For this case I'll use a VMware Workstation for Windows and VirtualBox for Linux as a virtualization platforms.

### Windows Part

1. Open FTK Imager and mount the .e01 image as a **physical** \(only\) device in **Writable** mode  

![](https://habrastorage.org/webt/lb/c6/lv/lbc6lvyxg1ezhi-lvzhv4bw4_uq.gif)

1. Notice a resulting device name. In this case it's a **PhysicalDrive3**
2. Open VMware Workstation and create a new VM, but **don't create a virtual disk** \(or remove one if exist\). You have to choose **Use a Physical Disk** in Virtual Machine Setting or add a new virtual disk as primary to the existing VM. You remember that our .e01 image is **PhysicalDrive3** now

![](https://habrastorage.org/webt/dp/4a/6f/dp4a6fqh_24o4ze2lbnv8xybvpi.gif)

1. So, you just need to start a VM and watching some IT magic  

![](https://habrastorage.org/webt/tl/k8/ad/tlk8adlpbniuw69wvv5msg6pa_g.gif)

## Arsenal Image Mounter

![Mount disk image](../.gitbook/assets/image%20%2847%29.png)

1. Select Mount disk image and select the file you want to mount
2. I usually select write temporary disk device

![](../.gitbook/assets/image%20%2848%29.png)

## Linux Part \(SIFT\)

1. The mostly typical tool using to attach .e01 images is ewfmount.py script. But there is a one hard limitation — this image being attached in **Read-only mode**. It's inappropriate for virtual machine. Therefore we'll use **xmount** command like:  

```text
sudo xmount --in ewf <path_to_image> --cache <path_to_cache_file> --out vdi <path_to_mount_point>
```

The main features of xmount for us — it mounts the image in Read-Write mode and it can take a lot of image types on input. You can check for xmount syntax [here](https://github.com/mika/xmount/blob/master/README).

![](https://habrastorage.org/webt/cf/lt/p7/cfltp73nepf_wxuf5gcph_vif98.gif)

1. Ok, now we have a .vdi image in /mnt/windows\_mount
2. Let's open a VirtualBox and create a new VM with our .vdi image \(choose existing disk\) as a primary disk

![](https://habrastorage.org/webt/l4/ly/fd/l4lyfdkcsloromsy4ilflmntqxi.gif)

1. Finally just boot up the VM and enjoy!  

![](https://habrastorage.org/webt/df/5m/mc/df5mmcf7s2rotceezw8htzgs0ui.gif)

