# Volatility

## Base Command

```text
$ python vol.py -f [name of image file] –profile=[profile] [plugin]
```

## System Profile

### imageinfo

```text
$ python vol.py -f ~/Desktop/win7_trial_64bit.raw imageinfo
```

The imageinfo output tells you the suggested profile that you should pass as the parameter to --profile=PROFILE when using other plugins. Since the profile tells volatility the format and type of memory objects that should be present in the RAM dump, getting the profile correct is an important first step before any further analysis.

```text
Suggested Profile(s) : Win7SP0x64, Win7SP1x64, Win2008R2SP0x64, Win2008R2SP1x64
                     AS Layer1 : AMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/Users/Michael/Desktop/win7_trial_64bit.raw)
                      PAE type : PAE
                           DTB : 0x187000L
                          KDBG : 0xf80002803070
          Number of Processors : 1
     Image Type (Service Pack) : 0
                KPCR for CPU 0 : 0xfffff80002804d00L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2012-02-22 11:29:02 UTC+0000
     Image local date and time : 2012-02-22 03:29:02 -0800
```

### kgdbscan

```text
$ python vol.py -f [image file name] kgdbscan
```

To further narrow down the most likely profile, the above command will use the kernel debugger data block scan plugin to make a profile suggestion based on the KDBG header.

## System Process

**Analysing System Process**

Volatility provides a few commands you can use for extracting information about processes:

* **pslist** finds and walks the doubly linked list of processes and prints a summary of the data. This method typically cannot show you terminated or hidden processes.
* **pstree** takes the output from pslist and formats it in a tree view, so you can easily see **parent and child relationships**.
* **psscan** scans for \_EPROCESS objects instead of relying on the linked list. This plugin can also find **terminated and unlinked \(hidden\) processes**.
* **psxview** locates processes using alternate process listings, so you can then crossreference different sources of information and reveal malicious discrepancies.

### pslist

```text
$ python vol.py -f lab.mem --profile=WinXPSP3x86 pslist
```

![output of the pslist command](../.gitbook/assets/image%20%2814%29.png)

* Three browsers are running \(two instances of IEXPLORE.EXE and one firefox .exe\), an e‑mail client \(thunderbird.exe\), and Adobe Reader \(AcroRd32.exe\). Thus, this machine is very likely to be a client or workstation, as opposed to a server.

  Furthermore, if you suspect a client-side attack vector \(such as a drive-by download or phishing exploit\), it is wise to mine these processes for data related to the incident because there’s a good chance that one or more of them was involved.

* All processes, including the system-critical ones, are running in session 0, which indicates this is an older \(Windows XP or 2003\) machine \(that is, before session 0 isolation\) and that only one user is currently logged on.
* Two of the AcroRd32.exe processes have 0 threads and an invalid handle table pointer \(indicated by the dashed lines\). If the exit time column were displayed \(we truncated it to prevent lines from wrapping on the page\), you’d see that these two processes have actually terminated. They’re “stuck” in the active process list because another process has an open handle to them \(see The Mis-leading Active in PsActiveProcessHead:[http://mnin.blogspot.com/2011/03/mis-leading-active-in.html](http://mnin.blogspot.com/2011/03/mis-leading-active-in.html)\).
* The process with PID 2280 \(a\[1\].php\) has an invalid extension for executables—it claims to be a PHP file. Furthermore, based on its creation time, it has a temporal relationship with several other processes that started during the same minute \(14:19:XX\), including a command shell \(cmd.exe\).

### pstree

```text
$ python vol.py -f lab.mem --profile=WinXPSP3x86 pstree
```

![](../.gitbook/assets/image%20%2810%29.png)

When viewing the processes as a tree, it’s much easier to determine the possible events that took place during the attack. You can see that firefox.exe \(PID 180\) was started by explorer.exe \(PID 1300\). This is normal—anytime you launch an application via the start menu or by double-clicking a desktop icon, the parent is Windows Explorer. It is also fairly common for browsers to create instances of Adobe Reader \(AcroRd32.exe\) to render PDF documents accessed via the web. The situation gets interesting when you see that AcroRd32.exe invoked a command shell \(cmd.exe\), which then started a\[1\].php.

### psscan

```text
python vol.py psscan –f memory.bin --profile=Win7SP1x64 --output=dot --output-file=processes.dot
```

![A diagram of processes involved in a malicious PDF exploit delivered via the web](../.gitbook/assets/image%20%282%29.png)

### Alternate process listings

* _Process object scanning_: This is the pool-scanning approach discussed in Chapter 5. Remember that the pool tags it finds are nonessential; thus, they can also be manipulated to evade the scanner.
* _Thread scanning_: Because every process must have at least one active thread, you can scan for \_ETHREAD objects and then map them back to their owning process. The member used for mapping is either \_ETHREAD.ThreadsProcess \(Windows XP and 2003\) or \_ETHREAD.Tcb.Process \(Windows Vista and later\). Thus, even if a rootkit manipulated the process’ pool tags to hide from psscan, it would also need to go

  back and modify the pool tags for all the process’ threads.

* _CSRSS handle table_: As discussed in the critical system process descriptions, csrss.exe is involved in the creation of every process and thread \(with the exception of itself and the processes that started before it\). Thus, you can walk this process’ handle table, as described later in the chapter, and identify all \_EPROCESS objects that way.
* _PspCid table_: This is a special handle table located in kernel memory that stores a reference to all active process and thread objects. The PspCidTable member of the kernel debugger data structure points to the table. Two rootkit detection tools, Blacklight and IceSword, relied on the PspCid table to find hidden processes. However, the author of FUTo \(see [http://www.openrce.org/articles/full\_view/19](http://www.openrce.org/articles/full_view/19)\) proved it was still possible to hide by removing processes from the table.
* _Session processes_: The SessionProcessLinks member of \_EPROCESS associates all processes that belong to a particular user’s logon session. It’s not any harder to unlink a process from this list, as opposed to the ActiveProcessLinks list. But because live system APIs don’t depend on it, attackers rarely find value in targeting it.
* _Desktop threads_: One of the structures discussed in Chapter 14 is the Desktop \(tagDESKTOP\). These structures store a list of all threads attached to each desktop, and you can easily map a thread back to its owning process.

## Event Log File

### Before Vista

**Finding Event Log File in Memory**

```text
$ python vol.py -f XPSP3.vmem --profile=WinXPSP3x86 pslist | grep services
```

```text
Volatility Foundation Volatility Framework 2.4 
0x81d97020 services.exe 692 648 16 352 0 0 2010-12-27 21:34:32
```

```text
$ python vol.py -f XPSP3.vmem --profile=WinXPSP3x86 vadinfo -p 69
```

**Extracting Event Log File in Memory**

```text
$ python vol.py -f cve2011_0611.dmp --profile=WinXPSP3x86 evtlogs -v --save-evt -D output/
```

The above uses the --save-evt option, the plugin created an .evt file \(raw binary event log\) and a .txt file \(parsed records in text format\) for each log file. The output of the parsed text file is in the following format:

```text
Date/Time | Log Name | Computer Name | SID | Source | Event ID | Event Type | Message Strings
```

```text
$ cat osession.txt
2011-04-10 09:14:22 UTC+0000|osession.evt|FINANCE1|N/A|Microsoft Office 12 Sessions|7000|Info|0;Microsoft Office Word;12.0.4518.1014;12.0.4518.1014;1368;0
2011-04-10 09:33:40 UTC+0000|osession.evt|FINANCE1|N/A|Microsoft Office 12 Sessions|7000|Info|0;Microsoft Office Word;12.0.6425.1000;12.0.6425.1000;1086;60
[snip]
2011-04-10 22:29:44 UTC+0000|osession.evt|FINANCE1|N/A|Microsoft Office 12 Sessions|7000|Info|0;Microsoft Office Word;12.0.6545.5000;12.0.6425.1000;80;60
2011-04-10 22:30:18 UTC+0000|osession.evt|FINANCE1|N/A|Microsoft Office 12 Sessions|7003|Warning|0;Microsoft Office Word;12.0.6545.5000;12.0.6425.1000
[snip]
```

### **Logging Policies**

```text
$ python vol.py -f XPSP3x86.vmem auditpol --profile=WinXPSP3x86

Volatility Foundation Volatility Framework 2.4
Auditing is Enabled
Audit System Events: S/F
Audit Logon Events: S/F
Audit Object Access: Not Logged
Audit Privilege Use: Not Logged
Audit Process Tracking: Not Logged
Audit Policy Change: S
Audit Account Management: S/F
Audit Dir Service Access: S/F
Audit Account Logon Events: S/F
```

### **Windows Vista, 2008, and 7 Event Logs**

Logs located on the disk at

```text
%systemroot%\system32\winevt\Logs
```

Note: To find the equivalent security IDs for Windows Vista, 2008, and 7 machines, add 4096 to the ID used for Windows XP/2003. For example, to find events that are related to someone logging on to a Windows 7 machine, the ID of interest would be **4624** instead of 528.

#### dumpfiles

You must extract the logs from memory using the **dumpfiles** plugin and then parse them with a tool external to Volatility. You can choose either a targeted methodology \(finding and dumping the event log of choice\) or you can choose to dump all event logs by making use of the dumpfiles plugin’s pattern matching \(regular expression\) capabilities.

```text
$ python vol.py –f Win7SP1x86.vmem --profile=Win7SP1x86 dumpfiles --regex .evtx$ --ignore-case --dump-dir output

Volatility Foundation Volatility Framework 2.4
DataSectionObject 0x8509eba8 756 \Device\HarddiskVolume1\Windows\System32\winevt\Logs\Microsoft-Windows-Diagnostics-Performance%4Operational.evtx
SharedCacheMap    0x8509eba8 756 \Device\HarddiskVolume1\Windows\System32\winevt\Logs\Microsoft-Windows-Diagnostics-Performance%4Operational.evtx
DataSectionObject 0x83eaec48 756 \Device\HarddiskVolume1\Windows\System32\winevt\Logs\Microsoft-Windows-Kernel-WHEA%4Errors.evtx
SharedCacheMap    0x83eaec48 756 \Device\HarddiskVolume1\Windows\System32\winevt\Logs\Microsoft-Windows-Kernel-WHEA%4Errors.evtx
[snip]
```

The following shows how to investigate one of these logs with the evtxdump.pl utility from Evtxparser:

```text
$ evtxdump.pl output/file.756.0x8404b008.vacb
```

Output of the command:

```text
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<Events>
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
<System>
<Provider Name="Microsoft-Windows-Application-Experience"
Guid="{EEF54E71-0661-422D-9A98-82FD4940B820}" />
<EventID>900</EventID>
<Version>0</Version>
<Level>4</Level>
<Task>0</Task>
<Opcode>0</Opcode>
<Keywords>0x0800000000000000</Keywords>
<TimeCreated SystemTime="1341520633" />
<EventRecordID>1</EventRecordID>
<Correlation />
<Execution ProcessID="3336" ThreadID="3580" />
[snip]
```

* Provider Name: Tells you from which log this information was extracted.
* EventID: Contains the event ID that you would look up online to figure out what event transpired.
* TimeCreated: A timestamp for when the event was generated.
* EventRecordID: The ID of the record, which helps you figure out the ordering of the generated records.

## Registry in Memory

Key information in registry:

* Hardware: Enumerate the external media devices that were connected to the system.
* User account information: Audit user passwords, accounts, most recently used \(MRU\) items, and user preferences.
* Recently run programs: Determine what applications executed recently \(using data from the Userassist, Shimcache, and MUICache keys\).
* System information: Determine system settings, installed software, and security patches that have been applied.
* Malware configurations: Extract data related to malware command and control sites, paths to infected files on disk, and encryption keys \(anything malicious code writes to the registry\).

### hivelist

The hivelist plugin scans for registry hives and then prints out their physical and virtual offsets and path information.

The following is an example:

```text
$ python vol.py -f win7.vmem --profile=Win7SP0x86 hivelist
```

```text
Volatility Foundation Volatility Framework 2.4
Virtual Physical Name
---------- ---------- ----
0x82b7a140 0x02b7a140 [no name]
0x820235c8 0x203675c8 \SystemRoot\System32\Config\SAM
0x87a1a250 0x27eb3250 \REGISTRY\MACHINE\SYSTEM
0x87a429d0 0x27f9d9d0 \REGISTRY\MACHINE\HARDWARE
0x87ac34f8 0x135804f8 \SystemRoot\System32\Config\DEFAULT
0x88603008 0x20d36008 \??\C:\Windows\ServiceProfiles\NetworkService\NTUSER.DAT
0x88691008 0x1ca1c008 \??\C:\Windows\ServiceProfiles\LocalService\NTUSER.DAT
0x9141e9d0 0x1dc569d0 \??\C:\Windows\System32\config\COMPONENTS
[snip]
```

### printkey

In the output, you can see the registry path, key name, last write time, subkeys, and any values that the key has \(in this case, there were none\). The printkey plugin also tells you whether the registry key or its subkeys are stable \(S\) or volatile \(V\).

```text
$ python vol.py -f win7.vmem --profile=Win7SP1x86 printkey -K "controlset001\control\computername"

Volatility Foundation Volatility Framework 2.4
Legend: (S) = Stable (V) = Volatile
----------------------------
Registry: \REGISTRY\MACHINE\SYSTEM
Key name: ComputerName (S)
Last updated: 2011-10-20 15:25:16
Subkeys:
(S) ComputerName
(V) ActiveComputerName
Values:
```

### Detecting Malware Persistence

These keys contain information about programs that run when the system boots up or a user logs in. Therefore, you should check these known registry keys to see if the malware is using them to persist on the machine. The following list shows some known startup keys.

* For system startup:

  ```text
  HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
  HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
  HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
  ```

* For user logons:

  ```text
  HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows
  HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows\Run
  HKCU\Software\Microsoft\Windows\CurrentVersion\Run
  HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
  ```

  An example of malware persistence is shown in the following output. The malicious executable C:\WINDOWS\system32\svchosts.exe is run every time the system starts up. This is immediately suspicious because no **svchosts.exe** executable exists on a clean Windows machine—it is attempting to blend in with the legitimate svchost.exe \(without the extra “s”\). Notice that you do not have to prefix the –K/--key argument with HKLM\SOFTWARE because it is actually not part of the path within the registry, but instead denotes which registry contains the key \(for example, the SOFTWARE hive on the local machine\).

```text
$ python vol.py -f grrcon.raw --profile=WinXPSP3x86 printkey -K "Microsoft\Windows\CurrentVersion\Run"

Volatility Foundation Volatility Framework 2.4
Legend: (S) = Stable (V) = Volatile
----------------------------
Registry: \Device\HarddiskVolume1\WINDOWS\system32\config\software
Key name: Run (S)
Last updated: 2012-04-28 01:59:22 UTC+0000
Subkeys:
(S) OptionalComponents
Values:
REG_SZ Adobe Reader Speed Launcher :
(S) "C:\Program Files\Adobe\Reader 9.0\Reader\Reader_sl.exe"
REG_SZ Adobe ARM :
(S) "C:\Program Files\Common Files\Adobe\ARM\1.0\AdobeARM.exe"
REG_SZ svchosts :
(S) C:\WINDOWS\system32\svchosts.exe
```

```text
$ python vol.py -f Win7.raw --profile=Win7SP1x64 printkey -K "SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUN"

Volatility Foundation Volatility Framework 2.4
Legend: (S) = Stable (V) = Volatile
----------------------------
Registry: \??\C:\Users\Andrew\ntuser.dat
Key name: Run (S)
Last updated: 2013-03-10 22:47:09 UTC+0000
Subkeys:
Values:
REG_SZ mswinnt : (S) "C:\Users\Andrew\Desktop\mswinnt.exe" 
--logfile=log.txt --encryption-index=4
```

## Network

```text
C:\> netstat -anob
```

### netscan

The primary Volatility plugin for determining network connections in Windows systems beyond Windows XP is the plugin. It will carve through the memory dump looking for artifacts from network activity, which means it may find sessions that were active or inactive at the time of the RAM dump.

```text
$ python vol.py -f win764bit.raw --profile=Win7SP0x64 netscan
```

![output of the netscan plugin](../.gitbook/assets/image%20%283%29.png)

