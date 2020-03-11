# Mounting an image to a VM

 For this case I'll use a VMware Workstation for Windows and VirtualBox for Linux as a virtualization platforms.  
  
 ## Windows Part  
  
1. Open FTK Imager and mount the .e01 image as a **physical** \(only\) device in **Writable** mode  
  
![](https://habrastorage.org/webt/lb/c6/lv/lbc6lvyxg1ezhi-lvzhv4bw4_uq.gif)  
  
2. Notice a resulting device name. In this case it's a **PhysicalDrive3**  
  
3. Open VMware Workstation and create a new VM, but **don't create a virtual disk** \(or remove one if exist\). You have to choose **Use a Physical Disk** in Virtual Machine Setting or add a new virtual disk as primary to the existing VM. You remember that our .e01 image is **PhysicalDrive3** now  
  
![](https://habrastorage.org/webt/dp/4a/6f/dp4a6fqh_24o4ze2lbnv8xybvpi.gif)  
  
4. So, you just need to start a VM and watching some IT magic  
  
![](https://habrastorage.org/webt/tl/k8/ad/tlk8adlpbniuw69wvv5msg6pa_g.gif)  

## Linux Part \(SIFT\) 

1. The mostly typical tool using to attach .e01 images is ewfmount.py script. But there is a one hard limitation — this image being attached in **Read-only mode**. It's inappropriate for virtual machine. Therefore we'll use **xmount** command like:  


```text
sudo xmount --in ewf <path_to_image> --cache <path_to_cache_file> --out vdi <path_to_mount_point>
```

  
The main features of xmount for us — it mounts the image in Read-Write mode and it can take a lot of image types on input. You can check for xmount syntax [here](https://github.com/mika/xmount/blob/master/README).  
  
![](https://habrastorage.org/webt/cf/lt/p7/cfltp73nepf_wxuf5gcph_vif98.gif)  
  
2. Ok, now we have a .vdi image in /mnt/windows\_mount  
  
3. Let's open a VirtualBox and create a new VM with our .vdi image \(choose existing disk\) as a primary disk  
  
![](https://habrastorage.org/webt/l4/ly/fd/l4lyfdkcsloromsy4ilflmntqxi.gif)  
  
4. Finally just boot up the VM and enjoy!  
  
![](https://habrastorage.org/webt/df/5m/mc/df5mmcf7s2rotceezw8htzgs0ui.gif)

