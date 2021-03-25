# Cloud Artifacts

## Dropbox

### Configuration

#### Windows XP
```
C:\Documents and Settings\%USERNAME%\Application Data\Dropbox\
C:\Documents and Settings\%USERNAME%\Local Settings\Application Data\Dropbox\
```
#### Windows Vista and later
```
C:\Users\%USERNAME%\AppData\Local\Dropbox\
C:\Users\%USERNAME%\AppData\Roaming\Dropbox\
```
#### Mac OS X
```
/Users/$USER/.dropbox/
```

#### Linux
```
/home/$USER/.dropbox/
```

* Configuration files are mostly encrypted

**host.dbx** and **host.db** is not encrypted and can be accessed, it contains the local folder name used to sync the account. The folder name is encoded in **Base64**

* **Filecache.dbx** located in the folder

```
C:\Documents and Settings\<username>\Application Data\Dropbox
```
* Windows Protection Folder
```
C:\Documents and Settings\<username>\Application Data\Microsoft\Protect
```
* Registry value
```
NTUSER.DAT\Software\Dropbox\ks\Client
```
* User’s password

### File Created

Executable and libraries are stored in
```
C:\Users\%USERNAME%\AppData\Roaming\Dropbox\bin
```

Four files created during installation
```
C:\Users\<username>\Desktop\Dropbox.lnk
C:\Users\<username>\Links\Dropbox.lnk
C:\Windows\Prefetch\DROPBOX N.N.NN.EXE-NNNNNNNN.pf
C:\Windows\Prefetch\DROPBOX.EXE-NNNNNNNN.pf
```

### Registry Changes

```
SYSTEM\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy\FirewallRules
SOFTWARE\Microsoft\CurrentVersion\Explorer\ShellIconOverlayIdentifiers\DropBoxExt1
SOFTWARE\Microsoft\CurrentVersion\Explorer\ShellIconOverlayIdentifiers\DropBoxExt1
SOFTWARE\Microsoft\CurrentVersion\Explorer\ShellIconOverlayIdentifiers\DropBoxExt1
NTUSER\Software\Microsoft\Windows\CurrentVersion\Uninstall\Dropbox
NTUSER\Software\Microsoft\Windows\CurrentVersion\UFH\SHC
NTUSER\Software\Dropbox\InstallPath
```

We can obtain from the industry
* Install Location
* Installed version

