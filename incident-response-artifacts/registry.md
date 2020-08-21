# Registry

## Registry Examination

### Online registry analysis
* Registry analysis in active system
* Checkable through RegEdit (regedit.exe), RegEdt32 (regedt32.exe) (http://support.microsoft.com/kb/141377)
### Offline registry analysis
* Registry analysis in inactive systems (forensic replication drives or images)
* Registry Hive file needs to be collected

![Registry Key and Value](../.gitbook/assets/image%20%2851%29.png)

The Data is stored in the main folders in a Tree like structure which is called Hive and its subfolders are called KEYS and SUBKEYS where each component’s configuration is stored called VALUES. 


|Root key |Abbreviation |Explanation |
| :--- | :--- |:--- |
|HKEY_CLASSES_ROOT |HKCR | HKLM\SOFTWARE\Classes and HKU\<SID>\Classes |
|HKEY_CURRENT_USER |HKCU |Subkey of the currently logged in user among the user profiles under HKU |
|HKEY_LOCAL_MACHINE |HKLM |Collection of hive files and memory hive existing on the system |
|HKEY_USERS |HKU |NTUSER.DAT file existing in the user root folder|
|HKEY_CURRENT_CONFIG|HKCC|Contents of HKLM\SYSTEM\CurrentControlSet\Hardware Profiles\Current|
|HKEY_PERFORMANCE_DATA|HKPD|Performance count (not accessible through the registry editor, accessible only with registry functions)|
