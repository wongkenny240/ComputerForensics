# Cloud Artifacts

## Dropbox

### Configuration

#### Windows XP

```text
C:\Documents and Settings\%USERNAME%\Application Data\Dropbox\
C:\Documents and Settings\%USERNAME%\Local Settings\Application Data\Dropbox\
```

#### Windows Vista and later

```text
C:\Users\%USERNAME%\AppData\Local\Dropbox\
C:\Users\%USERNAME%\AppData\Roaming\Dropbox\
```

#### Mac OS X

```text
/Users/$USER/.dropbox/
```

#### Linux

```text
/home/$USER/.dropbox/
```

* Configuration files are mostly encrypted

**host.dbx/ host.db**

**host.dbx** and **host.db** is not encrypted and can be accessed, it contains the local folder name used to sync the account. The folder name is encoded in **Base64**

**filecache.dbx and filecache.db**

* **Filecache.dbx** located in the folder

```text
C:\Documents and Settings\<username>\Application Data\Dropbox
```

* Windows Protection Folder

  ```text
  C:\Documents and Settings\<username>\Application Data\Microsoft\Protect
  ```

* Registry value

  ```text
  NTUSER.DAT\Software\Dropbox\ks\Client
  ```

* User’s password

The decrypted filecache.db contains:

* Server path
* Local file name
* Local creation time
* Local modified time
* Local size

![cloud\_entry\_table](../.gitbook/assets/image%20%2877%29.png)

![local\_entry\_table](../.gitbook/assets/image%20%2878%29.png)

### Installation

```text
SYSTEM\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy\FirewallRules
SOFTWARE\Microsoft\CurrentVersion\Explorer\ShellIconOverlayIdentifiers\DropBoxExt1
SOFTWARE\Microsoft\CurrentVersion\Explorer\ShellIconOverlayIdentifiers\DropBoxExt1
SOFTWARE\Microsoft\CurrentVersion\Explorer\ShellIconOverlayIdentifiers\DropBoxExt1
NTUSER\Software\Microsoft\Windows\CurrentVersion\Uninstall\Dropbox
NTUSER\Software\Microsoft\Windows\CurrentVersion\UFH\SHC
NTUSER\Software\Dropbox\InstallPath
```

Four files created during installation

```text
C:\Users\<username>\Desktop\Dropbox.lnk
C:\Users\<username>\Links\Dropbox.lnk
C:\Windows\Prefetch\DROPBOX N.N.NN.EXE-NNNNNNNN.pf
C:\Windows\Prefetch\DROPBOX.EXE-NNNNNNNN.pf
```

We can obtain from the registry

* Install Location
* Installed version

### File Created

Executable and libraries are stored in

```text
C:\Users\%USERNAME%\AppData\Roaming\Dropbox\bin
```

### Uninstall

* During the uninstall process the client config folder is removed
* The registry key NTUSER\Software\Dropbox is preserved \(but without values\)
* The prefetch files are not deleted
* Local copy of the file is not deleted

## Google Drive

Google Drive client is installed inside the Program Files folder

```text
C:\Program Files\Google\Drive
```

Client configuration is stored in the user profile, so we have different profiles for each user

```text
C:\Users\AppData\Local\Google\Drive
```

The default folder used for syncing files. By default, the folder is **empty**

```text
C:\Users\Google Drive
```

### Installation

During the installation different keys and values are created inside the registry

```text
SOFTWARE\Microsoft\Windows\CurrentVersion\Installer\Folders\
SOFTWARE\Google\Drive
NTUSER\Software\Microsoft\Windows\CurrentVersion\Run\GoogleDriveSync
NTUSER\Software\Classes
```

From the registry we can obtain:

* Installed version
* User folder

Four files are created during client installation:

```text
C:\Users\<username>\Desktop\Google Drive.lnk
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Google Drive\Google Drive.lnk
C:\Windows\Prefetch\GOOGLEDRIVESYNC.EXE-NNNNNNNN.pf
C:\Windows\Prefetch\GOOGLEUPDATE.EXE-NNNNNNNN.pf
```

### Configuration

* Configuration files are saved inside the installation folder in the user profile

Google provides a Mac OS X and Windows and desktop client.

**snapshot.db**

The **snapshot.db** is a SQLITE3 DB containing information about local and cloud entry

* Cloud\_entry table

  * File name
  * Created \(UNIX Timestamp\)
  * Modified \(UNIX Timestamp\)
  * URL
  * Checksum \(MD5 hash\)
  * Size
  * Shared

* Local\_entry
  * File name
  * Modified \(UNIX Timestamp\)
  * Checksum \(MD5 hash\)
  * Size
* After file deletion the file information is removed from the cloud\_entry and the local\_entry table

![](../.gitbook/assets/image%20%2880%29.png)

```text
C:\Users\%USERNAME%\AppData\Local\Google\Drive\snapshot.db
C:\Users\%USERNAME%\AppData\Local\Google\Drive\user_default\snapshot.db
```

**sync\_config.db**

The **sync\_config.db** is a SQLITE3 DB containing profile configuration

* Client version installed
* Local Sync Root Path
* User Email

```text
C:\Users\%USERNAME%\AppData\Local\Google\Drive\sync_config.db
C:\Users\%USERNAME%\AppData\Local\Google\Drive\user_default\sync_config.db
```

![](../.gitbook/assets/image%20%2879%29.png)

**sync\_config.log**

The Sync_log.log is a log file containing information about the client sync session
* Inside the file we can find information about
* Sync sessions
* File created
* File saved
* File deleted

```text
C:\Users\%USERNAME%\AppData\Local\Google\Drive\sync_config.log
C:\Users\%USERNAME%\AppData\Local\Google\Drive\sync_config.log.1
C:\Users\%USERNAME%\AppData\Local\Google\Drive\sync_config.log.2
C:\Users\%USERNAME%\AppData\Local\Google\Drive\user_default\sync_config.log
C:\Users\%USERNAME%\AppData\Local\Google\Drive\user_default\sync_config.log.1
C:\Users\%USERNAME%\AppData\Local\Google\Drive\user_default\sync_config.log.2
```

