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

## CurrentVersion

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

MS OFFICE usage trace
* Recently opened folder
```
HKU\{USER}\SOFTWARE\Microsoft\Office\{VERSION}\{APP}\Place MRU
```
* Recently used files
```
HKU\{USER}\SOFTWARE\Microsoft\Office\{VERSION}\{APP}\File MRU (Recent Files) 
```
* Saves various traces for each application and version
* Included information such as Recently opened folders, recently used files, recently used pages, recently accessed URLs, etc.
