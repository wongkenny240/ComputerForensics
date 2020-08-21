# Advanced EnCase

## Recover Partition

## Mounting Evidence as VFS

Virtual File System \(VFS\) mounts a drive, volume or folder as read-only offline network share.

![](../.gitbook/assets/image%20%2867%29.png)

1. Device &gt; Share &gt; Mount as Network Share
2. Input Server Info, client info

_Note: To stop the VFS service, double click “Virtual File System” in lower-right corner_

![](../.gitbook/assets/image%20%2869%29.png)



## Mount evidence as PDE

Mounting evidence by Physical Disk Emulation is like mounting the disk as an actual physical disk attached to the examiner machine. 

This enables analysis of the evidence using other forensic tools, or use it to boot into a virtual machine. But this limits the supported file systems for casual browsing to those supported by windows \(i.e. FAT & NTFS\)

![](../.gitbook/assets/image%20%2868%29.png)

1. Device &gt; Share &gt; Mount as Emulated Disk
2. Selecting “Disable Cache” enables write-emulation, and changes are sent to cache folder \(similar to mounting by FTK imager and Arsenal Image Mounter's "Write temporary disk device"\)

![](../.gitbook/assets/image%20%2866%29.png)

## Booting it into a VM

