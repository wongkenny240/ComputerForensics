# Registry

## Registry Examination

### Online registry analysis

* Registry analysis in active system
* Checkable through RegEdit \(regedit.exe\), RegEdt32 \(regedt32.exe\) \([http://support.microsoft.com/kb/141377](http://support.microsoft.com/kb/141377)\)

  **Offline registry analysis**

* Registry analysis in inactive systems \(forensic replication drives or images\)
* Registry Hive file needs to be collected

![Registry Key and Value](../.gitbook/assets/image%20%2851%29.png)

The Data is stored in the main folders in a Tree like structure which is called Hive and its subfolders are called KEYS and SUBKEYS where each component’s configuration is stored called VALUES.

| Root key | Abbreviation | Explanation |
| :--- | :--- | :--- |
| HKEY\_CLASSES\_ROOT | HKCR | HKLM\SOFTWARE\Classes and HKU\\Classes |
| HKEY\_CURRENT\_USER | HKCU | Subkey of the currently logged in user among the user profiles under HKU |
| HKEY\_LOCAL\_MACHINE | HKLM | Collection of hive files and memory hive existing on the system |
| HKEY\_USERS | HKU | NTUSER.DAT file existing in the user root folder |
| HKEY\_CURRENT\_CONFIG | HKCC | Contents of HKLM\SYSTEM\CurrentControlSet\Hardware Profiles\Current |
| HKEY\_PERFORMANCE\_DATA | HKPD | Performance count \(not accessible through the registry editor, accessible only with registry functions\) |

## CurrentVersion

![SOFTWARE\Microsoft\Windows\ CurrentVersion](../.gitbook/assets/image%20%2852%29.png)

'''
SOFTWARE\Microsoft\Windows CurrentVersion
'''
