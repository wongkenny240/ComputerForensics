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
