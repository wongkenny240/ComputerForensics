# Volatility

### Event Log File

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

The above uses the --save-evt option, the plugin created an .evt file (raw binary event log) and a .txt file (parsed records in text format) for each log file. The output of the parsed text file is in the following format:

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

**Logging Policies**

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

**Windows Vista, 2008, and 7 Event Logs**

Logs located on the disk at

```text
%systemroot%\system32\winevt\Logs
```

Note: To find the equivalent security IDs for Windows Vista, 2008, and 7 machines, add 4096 to the ID used for Windows XP/2003. For example, to find events that are related to someone logging on to a Windows 7 machine, the ID of interest would be **4624** instead of 528.

You must extract the logs from memory using the dumpfiles plugin and then parse them with a tool external to Volatility. You can choose either a targeted methodology (finding and dumping the event log of choice) or you can choose to dump all event logs by making use of the dumpfiles plugin’s pattern matching (regular expression) capabilities.

```text
$ python vol.py –f Win7SP1x86.vmem --profile=Win7SP1x86 dumpfiles --regex .evtx$ --ignore-case --dump-dir output

Volatility Foundation Volatility Framework 2.4
DataSectionObject 0x8509eba8 756 \Device\HarddiskVolume1\Windows\System32\winevt\Logs\Microsoft-Windows-Diagnostics-Performance%4Operational.evtx
SharedCacheMap 0x8509eba8 756 \Device\HarddiskVolume1\Windows\System32\winevt\Logs\Microsoft-Windows-Diagnostics-Performance%4Operational.evtx
DataSectionObject 0x83eaec48 756 \Device\HarddiskVolume1\Windows\System32\winevt\Logs\Microsoft-Windows-Kernel-WHEA%4Errors.evtx
SharedCacheMap 0x83eaec48 756 \Device\HarddiskVolume1\Windows\System32\winevt\Logs\Microsoft-Windows-Kernel-WHEA%4Errors.evtx
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

### Registry in Memory

Key information in registry:

* Hardware: Enumerate the external media devices that were connected to the system.
* User account information: Audit user passwords, accounts, most recently used (MRU) items, and user preferences.
* Recently run programs: Determine what applications executed recently (using data from the Userassist, Shimcache, and MUICache keys).
* System information: Determine system settings, installed software, and security patches that have been applied.
* Malware configurations: Extract data related to malware command and control sites, paths to infected files on disk, and encryption keys (anything malicious code writes to the registry).

#### hivelist

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

#### printkey

In the output, you can see the registry path, key name, last write time, subkeys, and any values that the key has (in this case, there were none). The printkey plugin also tells you whether the registry key or its subkeys are stable (S) or volatile (V).

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

#### Detecting Malware Persistence

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
An example of malware persistence is shown in the following output. The malicious executable C:\WINDOWS\system32\svchosts.exe is run every time the system starts up. This is immediately suspicious because no **svchosts.exe** executable exists on a clean Windows
machine—it is attempting to blend in with the legitimate svchost.exe (without the extra “s”). Notice that you do not have to prefix the –K/--key argument with HKLM\SOFTWARE because it is actually not part of the path within the registry, but instead denotes which
registry contains the key (for example, the SOFTWARE hive on the local machine).

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
