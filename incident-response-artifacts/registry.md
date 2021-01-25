# Registry

## Registry Examination

### Online registry analysis

* Registry analysis in active system
* Checkable through RegEdit \(regedit.exe\), RegEdt32 \(regedt32.exe\) \([http://support.microsoft.com/kb/141377](http://support.microsoft.com/kb/141377)\)

### Offline registry analysis

* Registry analysis in inactive systems \(forensic replication drives or images\)
* Registry Hive file needs to be collected

![Registry Key and Value](../.gitbook/assets/image%20%2851%29.png)

The Data is stored in the main folders in a Tree like structure which is called Hive and its subfolders are called KEYS and SUBKEYS where each component’s configuration is stored called VALUES.

| Root key | Abbreviation | Explanation |
| :--- | :--- | :--- |
| HKEY\_CLASSES\_ROOT | HKCR | HKLM\SOFTWARE\Classes and HKU\Classes |
| HKEY\_CURRENT\_USER | HKCU | Subkey of the currently logged in user among the user profiles under HKU |
| HKEY\_LOCAL\_MACHINE | HKLM | Collection of hive files and memory hive existing on the system |
| HKEY\_USERS | HKU | NTUSER.DAT file existing in the user root folder |
| HKEY\_CURRENT\_CONFIG | HKCC | Contents of HKLM\SYSTEM\CurrentControlSet\Hardware Profiles\Current |
| HKEY\_PERFORMANCE\_DATA | HKPD | Performance count \(not accessible through the registry editor, accessible only with registry functions\) |

### CurrentVersion

![SOFTWARE\Microsoft\Windows CurrentVersion](../.gitbook/assets/image%20%2852%29.png)

```text
SOFTWARE\Microsoft\Windows\CurrentVersion
```

### Last logged in user

```text
HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
```

* _**DefaultUserName**_ value represents the last logged in user

![](../.gitbook/assets/image%20%2854%29.png)

### Program Usage Log

* List of files opened in Paint

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Applets\Paint\Recent File List
```

File{\#Number}–The lower the number, the most recently opened file \(saving the value at the point of exiting Paint\)

![](../.gitbook/assets/image%20%2853%29.png)

### Microsoft Office usage trace

* Recently opened folder

  ```text
  HKU\{USER}\SOFTWARE\Microsoft\Office\{VERSION}\{APP}\Place MRU
  ```

* Recently used files

  ```text
  HKU\{USER}\SOFTWARE\Microsoft\Office\{VERSION}\{APP}\File MRU
  ```

* Saves various traces for each application and version
* Included information such as Recently opened folders, recently used files, recently used pages, recently accessed URLs, etc.

![File MRU with Registry Explorer](../.gitbook/assets/image%20%2855%29.png)

### Search term list \(Explorer\)

#### Windows 7

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery
```

* List of search terms when using search in Windows 7 Explorer
* Vista does not store the search term list in the registry.
* Check the order of search word usage through the MRUListEx key value
* 10 -&gt; 0F -&gt; 0E -&gt; 0D -&gt; 0C -&gt; 0B -&gt; 0A -&gt; 04 -&gt; 09 -&gt; 08 -&gt; 07 -&gt; 06 -&gt; 05 -&gt; 03 -&gt; 02 -&gt; 01 -&gt; 00

### Recently opened files \(Explorer\)

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
```

* Files such as recently opened documents, pictures, music, and videos
* 2000/XP – My Recent Documents
* Vista/7 – Recent Items
* Check the order of search word usage through the MRUListEx key value

### Recently executed command \(Explorer\)

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RunMRU
```

* List of commands executed through “Start -&gt; Run” or “Ctrl + R”
* The order of the most recently executed commands is the alphabetical order of the MRUList.

![](../.gitbook/assets/image%20%2856%29.png)

### Typed Paths \(Explorer\)

### UserAssist

### USB

USB storage medium identification procedure

1. When the USB storage medium is connected, the bus driver is sent to the PnP administrator.
2. Connection notification using device's unique identification number \(device descriptor\)
3. Device descriptor - includes manufacturer, serial number, driver information, etc.
4. PnP administrator sets Device Class ID based on received information and searches for appropriate driver
5. If there is no driver, the PnP administrator in user mode receives the driver from the firmware of the device, loads it, and writes it to the registry.

```text
HKLM\SYSTEM\ControlSet00X\Enum\USBSTOR\{DID, device class identifier}
HKLM\SYSTEM\ControlSet00X\Control\DeviceClasses\{GUID}
```

1. The device driver installation process is saved in a log file.
2. As a result, traces of USB devices can be identified through log files \(setupapi.log\) and registry.

Precautions when checking registry key last modification time information

* Each registry key stores the last modification time of the corresponding key. 
* Various traces of the USB can be identified by using the last modification time information, but the time of the Enum USB, Enum USBSTOR subkeys should not be considered. 
* According to the security policy \(Windows Vista/7\), the PnP administrator frequently accesses to set the sub-key security token. 
  * RegSetKeySecurityAPI call -&gt; change the last modification time

#### Storage media information

```text
HKLM\SYSTEM\ControlSet00X\Enum\USBSTOR
```

* Show manufacturer, product name, and version information through Device Class ID format

#### Serial number

```text
HKLM\SYSTEM\ControlSet00X\Enum\USBSTOR\{Device Class ID}
```

* Check the serial number through the Unique Instance ID format of the Device Class ID subkey

![](../.gitbook/assets/image%20%2857%29.png)

#### Manufacturer ID, Product ID

```text
HKLM\SYSTEM\ControlSet00X\Enum\USB
```

* VID_\#\#\#\#&PID_\#\#\#\# -&gt; Manufacturer ID, Product ID

![](../.gitbook/assets/image%20%2858%29.png)

#### Connected volume name

```text
HKLM\SOFTWARE\Microsoft\Windows Portable Devices\Devices
```

Under Devices, search for a key including product name or serial number among subkeys

_**FriendlyName**_

![](../.gitbook/assets/image%20%2860%29.png)

![](../.gitbook/assets/image%20%2859%29.png)

