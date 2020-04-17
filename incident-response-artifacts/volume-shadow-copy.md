# Volume Shadow Copy

Vista/Win7/Win8 now logs changes to the entire Volume and keeps track of the specific clusters that are changed on a daily basis in the new Volume Snapshot Service or VSS. 

Vista/Win7 Business, Enterprise, and Ultimate have Shadow Copy enabled by default. 

Enables a user to: 
* Revert the file to any previous version 
* Restore a previous version from backup 
* Make a copy of previous version 

All volume shadow copy files are stored in the ‘System Volume Information’ folder on the root of the volume and are recognizable by their names. 

The number ***3808876b-c176-4e48-b7ae-04046e6cc752***, is a unique identifier specific to the volume shadow service.

## System Snapshot Frequency
### Windows Vista,
The system snapshot is scheduled to take place every ***24 hours***. 

### Windows 7
The system snapshot is scheduled to take place every ***7 days***.

You may notice that this is not exact. Windows Vista will not take volume snapshots exactly every 24 hours; there may be some time changes day to day. This is because the VSS will create new shadow copies only once the computer has been idle for a certain amount of time, or the computer is being turned off or rebooted.

## Tools that can parse the volume shadow copy are:
### Magnet forensics IEF
### VSC-Toolset 
http://dfstream.blogspot.com/p/vsc-toolset.html
### libvshadow (SIFT) 
http://digitalforensics.sans.org/community/downloads
### ShadowExplorer


