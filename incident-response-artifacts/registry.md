# Registry

## Registry Examination

### Online registry analysis

* Registry analysis in active system
* Viewable through RegEdit \(regedit.exe\), RegEdt32 \(regedt32.exe\) \([http://support.microsoft.com/kb/141377](http://support.microsoft.com/kb/141377)\)

The Data is stored in the main folders in a Tree like structure which is called Hive and its subfolders are called KEYS and SUBKEYS where each component’s configuration is stored called VALUES.

| Root key | Abbreviation | Explanation |
| :--- | :--- | :--- |
| HKEY\_CLASSES\_ROOT | HKCR | HKLM\SOFTWARE\Classes and HKU\Classes |
| HKEY\_CURRENT\_USER | HKCU | Subkey of the currently logged in user among the user profiles under HKU |
| HKEY\_LOCAL\_MACHINE | HKLM | Collection of hive files and memory hive existing on the system |
| HKEY\_USERS | HKU | NTUSER.DAT file existing in the user root folder |
| HKEY\_CURRENT\_CONFIG | HKCC | Contents of HKLM\SYSTEM\CurrentControlSet\Hardware Profiles\Current |
| HKEY\_PERFORMANCE\_DATA | HKPD | Performance count \(not accessible through the registry editor, accessible only with registry functions\) |

![Registry Key and Value](../.gitbook/assets/image%20%2851%29.png)

### Offline registry analysis

* Registry analysis in inactive systems \(forensic replication drives or images\)
* Registry Hive file needs to be collected

#### Registry extraction

* Collect registry location - Export Files
* Use FTK Imager to export the folder in Windows/System32/config

![](../.gitbook/assets/image%20%2886%29.png)

#### Regripper

* Select the corresponding registry and the report location

![](../.gitbook/assets/image%20%2888%29.png)

* Continue to load the other remaining registry files \(e.g. Security, Software, System, NTUSER.dat\)

#### Registry Explorer

* Open the Registry Explorer \(Eric Zimmerman\)
* Select the Registry to view

![](../.gitbook/assets/image%20%2887%29.png)

#### System specific hive

Windows maintains five main registry hives in the path below:

```text
%SYSTEMROOT%\system32\config
```

Hive files name

```text
SYSTEM, SECURITY, SOFTWARE, SAM, DEFAULT.
```

#### User specific hive

| Version | Path |
| :--- | :--- |
| Windows XP and Server 2003 | • \Documents and Settings\NTUSER.DAT    • \Documents and Settings\Local Settings\Application Data\Microsoft\Windows\USRCLASS.DAT |
| Windows Vista, 7, and Server 2008 | • \Users\NTUSER.DAT    • \Users\AppData\Local\Microsoft\Windows\USRCLASS.DAT |

#### Mapping

| Rootkey | Files |
| :--- | :--- |
| HKLM\Software | SOFTWARE |
| HKLM\Security | SECURITY |
| HKLM\System | SYSTEM |
| HKLM\SAM | SAM |
| HKU.DEFAULT | DEFAULT |
| HKU{SID} | NTUSER.DAT |
| HKU{SID}\_Classes | USRCLASS.DAT |
| HKEY\_CURRENT\_CONFIG | HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Hardware Profiles\XXXX \(i.e. HKLM\SYSTEM\ControlSetXXX\) |

### System Configuration Registry Keys

| Key | Value | Description |
| :--- | :--- | :--- |
| HKLM\System\CurrentControlSet\Control\Computername | Computername, AciveComputername |  |
| HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion |  | Basic information about the version of the Windows |

#### CurrentVersion

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

1. The device **driver installation process** is **saved in a log file**.
2. As a result, traces of USB devices can be identified through log files \(**setupapi.log**\) and registry.

Precautions when checking registry key last modification time information

* Each registry key stores the last modification time of the corresponding key. 
* Various traces of the USB can be identified by using the last modification time information, but the time of the Enum USB, Enum USBSTOR subkeys should not be considered. 
* According to the security policy \(Windows Vista/7\), the PnP administrator frequently accesses to set the sub-key security token. 
  * RegSetKeySecurityAPI call -&gt; change the last modification time

#### USB Registry Keys

```text
HKLM\SYSTEM\ControlSet00X\Enum\USBSTOR
```

* Show manufacturer, product name, and version information through Device Class ID format
* For Example Ven\_&lt;Manufacturer&gt;&&lt;Product Name&gt;&Rev\_&lt;Version&gt;

![](../.gitbook/assets/image%20%28107%29.png)

#### Serial number

```text
HKLM\SYSTEM\ControlSet00X\Enum\USBSTOR\{Device Class ID}
```

* The serial number is a sub-key of the Device Class ID
* If the USB devices have a unique serial from their respective manufacturers. &0 or &1 will be displayed at the end of the serial number. 
* If instead the second character is an & then the device does not have a unique serial number and Windows has issued one which is unique to the local system only.

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

![](../.gitbook/assets/image%20%28103%29.png)

_**FriendlyName**_

![](../.gitbook/assets/image%20%2860%29.png)

![](../.gitbook/assets/image%20%2859%29.png)

In this example, the Volume Name is KINGSTON

![](../.gitbook/assets/image%20%28105%29.png)

One more example the Volume Name is FOR408-USB

If there's not Serial Number in like the second key, then we go to the following key to look for the bracket value \(i.e. {c0b076c....}\)

![](../.gitbook/assets/image%20%28104%29.png)

![](../.gitbook/assets/image%20%28106%29.png)

