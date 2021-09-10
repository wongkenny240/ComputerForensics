# LNK File

LNK files \(labels or Windows shortcut files\) are typically files which are created by the Windows OS automatically, whenever a user opens their files. These files are used by the operating system to secure quick access to a certain file. In addition, some of these files can be created by users themselves to make their activities easier.

## Location

Most of LNK-files are located on the following paths:

### Windows 7 to 10

```text
C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent
```

### Windows XP

```text
C:\Documents and Settings\%USERNAME%\Recent
```

### Other location

However, there many other places where investigators can find LNK files:

```text
On the desktop (such shortcuts are usually created by users to secure quick access to documents and apps)
C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Office\Recent\ (for Microsoft Office documents on Windows 7 to 10)
C:\Users\%USERNAME%\Downloads (Sometimes users send shortcuts via e-mails to other users instead of the documents to be delivered. Consequently, other users download those shortcuts. Again, this is for Windows 7 to 10)
Startup folder
```

Windows Vista, 7, and 2008

```text
C:\Documents and Settings\%USERNAME%\Recent\
C:\Documents and Settings\%USERNAME%\ApplicationData\Microsoft\Office\Recent\
```

Windows XP and 2000:

```text
C:\Users\%USERNAME%\AppData\ Roaming\Microsoft\Windows\Recent\
C:\Users\%USERNAME%\AppData\ Roaming\Microsoft\Office\Recent\
```

## Tools

### Windows LNK Parsing Utility \(lp\) – TZWorks

{% embed url="https://www.tzworks.net/prototype\_page.php?proto\_id=11" caption="" %}

### Lnkanalyser – Mark Woan

{% embed url="http://www.woanware.co.uk/forensics/lnkanalyser.html" caption="" %}

### Using the Link File Parser in EnCase

* Windows Artifact Parser -&gt; Link files
* Case Analyzer to analysis
* Link files can be stored in RAM memory and the OS writes volatile data that is not currently in use to swap file \(**pagefile.sys**\)
* In **Windows XP/Vista/7**, if the system is placed into **hibernation** or hybrid sleep, the contents of RAM are written to the hiberfil.sys file
* The swap file is configured to adjust in size. While this adjustment occurs, clusters that were formerly allocated to the swap file find themselves in unallocated space, therefore you should **parse for link files in the unallocated spaces**.

![Select Link files &amp;gt; Search Unallocated](../.gitbook/assets/image%20%28138%29.png)

