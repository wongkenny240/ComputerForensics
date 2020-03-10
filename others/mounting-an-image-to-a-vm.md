# Mounting an image to a VM

 For this case I'll use a VMware Workstation for Windows and VirtualBox for Linux as a virtualization platforms.  
  
**Windows Part**  
  
1. Open FTK Imager and mount the .e01 image as a **physical** \(only\) device in **Writable** mode

![](../.gitbook/assets/image%20%285%29.png)

 2. Notice a resulting device name. In this case it's a **PhysicalDrive3**  
  
3. Open VMware Workstation and create a new VM, but **don't create a virtual disk** \(or remove one if exist\). You have to choose **Use a Physical Disk** in the Virtual Machine Settings or add a new virtual disk as primary to the existing VM. You remember that our .e01 image is **PhysicalDrive3** now

![](../.gitbook/assets/image%20%2812%29.png)

4. So, you just need to start a VM 

![](../.gitbook/assets/image%20%2813%29.png)

