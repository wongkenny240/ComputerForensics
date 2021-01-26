---
description: Below list out a list of procedures to create computer images
---

# Acquisition Method

## Encryption Detection \(EDD.exe\)

A good practice is to check for encryption before performing acquisition to avoid running into trouble

One good tool to peform such task is EDD.exe by magnet forensic

Just run the EDD.exe and it will tell you which volume is encrypted.

![](../.gitbook/assets/image%20%2849%29.png)

## Memory Acquisition \(FTK Imager Lite\)

File &gt; Capture Memory

![FTK Imager Lite for capturing memory](../.gitbook/assets/2019-04-04-17_31_52-greenshot.png)

## FastBloc SE

1. Make sure no devices are attached \(or only your storage device is attached\)
2. Tools &gt; FastBloc SE &gt; Write Blocked
3. Attach the target device to the system
4. In EnCase, either create a new case or open an existing one
5. Add Evidence &gt; Add Local Device
6. On the page that follows, accept the defaults and click Next. On the screen that follows, you will see a dot or Yes in the Write Blocked column, and the icon for the device will have a green box around it, both indicating a successful write block.
7. Select the write-blocked target device \(blue check\) &gt; Finish &gt; double click the evidence &gt; Acquire

{% hint style="info" %}
Write Block = writes are prevented but are cached locally to prevent Windows error messages

Write Protect = writes are prevented, nothing is cached locally, and Windows launches error messages when writes are attempted
{% endhint %}

![](../.gitbook/assets/image%20%2862%29.png)

![Acquire &amp;gt; Acquire](../.gitbook/assets/image%20%2863%29.png)

![Remove Write-Blocking after complete the acquisition](../.gitbook/assets/image%20%2864%29.png)

After finished acquiring &gt; Physically remove the device &gt; Stop the write-blocking software in EnCase \(Tools &gt; FastBloc SE &gt; Clear All\)

## Tableau Write Blocker

1. Connect the target disk to the write blocker 
2. In EnCase, either create a new case or open an existing one
3. Add Evidence &gt; Add Local Device
4. Select the device that is write-blocked
5. In the Evidence tab, right click the item we would like to acquire, Select Process Evidence -&gt; Acquire

![Detect Tableau Hardware](../.gitbook/assets/image%20%2822%29.png)

![Process Evidence -&amp;gt; Acquire](../.gitbook/assets/image%20%2816%29%20%282%29.png)

![Location tab](../.gitbook/assets/image%20%286%29%20%281%29%20%282%29%20%282%29.png)

![Format tab](../.gitbook/assets/image%20%287%29.png)

![Advanced tab](../.gitbook/assets/image%20%281%29.png)

## Tableau Duplicator

## LinEn \(Linux\)

{% hint style="info" %}
Edit the inittab file with text editor to change your Linux \(e.g. Helix\) to console mode by changing `id:5:initdefault:.` to `id:3:initdefault:.`
{% endhint %}

1. Attached the target drive to the Linux imaging platform
2. Attached storage drive \(FAT32\) to the Linux imaging platform
3. Boot your Linux machine to console and log in as root
4. Check what file systems are mounted

   ```bash
   mount
   ```

5. Check what devices are available

   ```text
   fdisk -l
   ```

6. Mount your storage drive and check that the storage drive is mounted

   ```text
   mkdir /mnt/fat32
   mount /dev/hda1 /mnt/fat32
   mount
   ```

7. Create the folder on your storage volume to hold the EnCase evidence file
8. Go to the directory of LinEn and run LinEn

   ```text
   ./LinEn
   ```

9. press `A` / use Tab key to go to Acquire and press Enter
10. Select your drive and press Enter
11. Choose the path for your evidence file and prefix it with the path to the mount path e.g. `/case/casename/evidence` to `/mnt/winfat/cases/casename/evidence/XXX001`

## Guymager \(Caine OS\)

1. Insert the CAINE OS USB into the target machine. Boot from BIOS \(F2\). Select the USB as the boot drive
2. After startup, connect storage harddisk to the target machine
3. Mount storage harddisk Create mount point

   ```text
    mkdir /media/drive
   ```

   Mount Drive in RW mode

   ```text
    sudo mount /dev/sdc2 /media/drive -rw
   ```

4. Open guymager and select Calculate MD5 and Verify image after acquisition \(takes twice as long\)
5. Click OK to start the acquisition 

![Fill in the information and click OK](../.gitbook/assets/image%20%2818%29%20%283%29%20%283%29.png)

## Convert a hibernation file to a memory dump

A hibernation file is stored in C:\hiberfile.sys if you have hibernation enabled. It contains parts of the memory at the time of hibernation, depending on the version of Windows. Run this to covert it to a raw image for further processing with Volatility.

```text
volatility -f /path/to/hiberfile.sys --profile=<profile> imagecopy -O /path/to/output/folder/hibermemory.raw
```

## Remote Acquisition

