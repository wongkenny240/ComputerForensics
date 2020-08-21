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

Program Usage Log

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

### Last logged in user

```text
HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
```

* _**DefaultUserName**_ value represents the last logged in user

![](../.gitbook/assets/image%20%2854%29.png)


### Search term list

#### Windows 7 
```
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery
```

* List of search terms when using search in Windows 7 Explorer
* Vista does not store the search term list in the registry.
* Check the order of search word usage through the MRUListEx key value
* 10 -> 0F -> 0E -> 0D -> 0C -> 0B -> 0A -> 04 -> 09 -> 08 -> 07 -> 06 -> 05 -> 03 -> 02 -> 01 -> 00


### Recently opened files
```
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
```

* Files such as recently opened documents, pictures, music, and videos
* 2000/XP – My Recent Documents
* Vista/7 – Recent Items
* Check the order of search word usage through the MRUListEx key value

### Recently executed command

```
HKU\{USER}\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RunMRU 
```
* List of commands executed through “Start -> Run” or “Ctrl + R”


### USB

