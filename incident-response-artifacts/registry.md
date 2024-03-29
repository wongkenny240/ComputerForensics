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

### MRUs

#### Recently opened files \(Explorer\)

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
```

This key can contain quite a number of values, all of which are binary data types. We are interested in the values that have numbers as names, which contain the names of the files accessed \(in Unicode\), and the value named **MRUListEx**, which records the order in which the files were accessed \(as DWORDs\). Given that adding a value and its associated data to the key, as well as modifying the MRUListEx value, constituted modifying the key, the **LastWrite time of the RecentDocs key will tell us when that file was accessed**.

* Files such as recently opened documents, pictures, music, and videos
* 2000/XP – My Recent Documents
* Vista/7 – Recent Items
* Check the order of search word usage through the MRUListEx key value

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.MOV
```

The RecentDocs key also has a number of subkeys, each one being the extension of a file that was opened \(.doc, .txt, .html, etc.\). The values within these subkeys are maintained in the same way as in the RecentDocs key: The value names are numbered, and their data contains the name of the file accessed as a binary data type \(in Unicode\). Another value called MRUListEx is also a binary data type and maintains the order in which the files were accessed, most recent first, as DWORDs.

![](../.gitbook/assets/image%20%28131%29.png)

#### Recently executed command \(Explorer\)

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RunMRU
```

* List of commands executed through “Start -&gt; Run” or “Ctrl + R”
* The order of the most recently executed commands is the alphabetical order of the MRUList.

![](../.gitbook/assets/image%20%2856%29.png)

![](../.gitbook/assets/image%20%28130%29.png)

**The MRUList value within the RunMRU key tells** us that the most recent item to be typed into the Run box is item "e"

* List of files opened in Paint

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Applets\Paint\Recent File List
```

File{\#Number}–The lower the number, the most recently opened file \(saving the value at the point of exiting Paint\)

![](../.gitbook/assets/image%20%2853%29.png)

#### Microsoft Office usage trace

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

#### Search term list \(Explorer\)

**Windows 7**

```text
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery
```

* List of search terms when using search in Windows 7 Explorer
* Vista does not store the search term list in the registry.
* Check the order of search word usage through the MRUListEx key value
* 10 -&gt; 0F -&gt; 0E -&gt; 0D -&gt; 0C -&gt; 0B -&gt; 0A -&gt; 04 -&gt; 09 -&gt; 08 -&gt; 07 -&gt; 06 -&gt; 05 -&gt; 03 -&gt; 02 -&gt; 01 -&gt; 00

#### Typed Paths \(Explorer\)

```text
HKU\{USER}\SOFTWARE\Microsoft\Internet Explorer\TypedURLs
```

The TypedURLs key maintains a list of the URLs the user types into the Address bar in Internet Explorer. However, the value names within the TypedURLs key are ordered with the most recently typed URL having the lowest number; consequently, this key doesn’t have an MRUList or MRUListEx value.

![](../.gitbook/assets/image%20%28132%29.png)

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

#### Serial number

![](../.gitbook/assets/image%20%28107%29.png)

```text
HKLM\SYSTEM\ControlSet00X\Enum\USBSTOR\{Device Class ID}
```

* Device Class ID format show manufacturer, product name, and version information 
* For Example Ven\_&lt;Manufacturer&gt;&&lt;Product Name&gt;&Rev\_&lt;Version&gt;

![](../.gitbook/assets/image%20%28109%29.png)

* The serial number is a sub-key of the Device Class ID

![](../.gitbook/assets/image%20%28108%29.png)

* If the USB devices have a unique serial from their respective manufacturers. &0 or &1 will be displayed at the end of the serial number. 
* If instead the second character is an & then the device does not have a unique serial number and Windows has issued one which is unique to the local system only.

![](../.gitbook/assets/image%20%28110%29.png)

![](../.gitbook/assets/image%20%2857%29.png)

#### Vendor ID, Product ID

```text
HKLM\SYSTEM\ControlSet00X\Enum\USB
```

* VID_\#\#\#\#&PID_\#\#\#\# -&gt; Vendor ID, Product ID

![](../.gitbook/assets/image%20%2858%29.png)

#### Connected volume name

```text
HKLM\SOFTWARE\Microsoft\Windows Portable Devices\Devices
```

Under Devices, search for a key including product name or serial number among subkeys

![](../.gitbook/assets/image%20%28103%29.png)

_**FriendlyName \(i.e. Volume Name\)**_

![](../.gitbook/assets/image%20%2860%29.png)

![](../.gitbook/assets/image%20%2859%29.png)

In this example, here the **FriendlyName** \(i.e. Volume Name\) is KINGSTON

![](../.gitbook/assets/image%20%28105%29.png)

One more example, here the **FriendlyName** \(i.e. Volume Name\) is FOR408-USB

If there's not Serial Number in like the second key, then we go to the following key to look for the bracket value \(i.e. {c0b076c....}\)

```text
SYSTEM\CurrentControlSet\Enum\USBSTOR\<Device>\<SerialNumber>\Device Parameters\Partmgr
```

![1. Find the value in the USB TOR Key ](../.gitbook/assets/image%20%28127%29.png)

![2. Find the USB under the Devices Key](../.gitbook/assets/image%20%2870%29.png)

![3. Look up the FriendlyName of the Key](../.gitbook/assets/image%20%28128%29.png)

Then we can correlate to the value under Windows Portable Devices with the bracket value

#### Volume Serial Number

* VSN is created by Windows Vista and up Operating Systems each time the device is formatted. 

```text
SOFTWARE\Microsoft\Windows NT\CurrentVersion\EMDMgmt
```

![](../.gitbook/assets/image%20%28129%29.png)

This is a Decimal value of the Volume Serial Number, which is a **Hexadecimal value**. Convert this value into the Hex and you have your Volume Serial Number.

You can check with the **vol** command with the device connected.

_Note: The Volume Serial Number can change for the device if it is formatted, as the Volume Serial Number is allocated after the Format._

_Note: It is important to make note of the Volume Serial Number and the Volume Name for use in analysing the Link \(.lnk\) files_

#### Determine the Drive Letter

```text
SYSTEM\MountedDevices
```

* When a USB removable storage device is connected to a Windows system, it is assigned a drive letter; that drive letter shows up in the MountedDevices key. 
* If the device is assigned the drive letter F:\, the value in the MountedDevices key will appear as \DosDevices\F:. 
* We can map the entry from the USBSTOR key to the MountedDevices key using the **ParentldPrefix** value found within the unique instance ID key for the device. 

![](../.gitbook/assets/image%20%28134%29.png)

