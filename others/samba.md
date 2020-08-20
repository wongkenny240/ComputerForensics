# Samba

Using command line tools requires two separate operations:

* Partitioning the drive.
* Creating the file system\(s\).

GParted combines both of these into one coordinated interface.

![](../.gitbook/assets/image%20%2850%29.png)

Select &lt;New&gt; 

Edit samba configuration \(_/etc/samba/smb.conf_\)

Change the path to the new partition or the path you want to share.

> _/etc/samba/smb.conf_

`[global]  
workgroup = workgroup  
security = share  
encrypt password = yes  
smb passwd file = /etc/samba/smbpasswd  
show add printer wizard = No  
wins support = no`

`[files]  
path = /media/sdb1/files  
guest ok = yes  
read only = no  
available = yes  
browsable = yes  
public = yes  
writable = yes`

