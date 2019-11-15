# Volatility

#### Event Log File

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
$ python vol.py –f Win7SP1x86.vmem --profile=Win7SP1x86 dumpfiles --regex .evtx$ --ignore-case
--dump-dir output
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

• Provider Name: Tells you from which log this information was extracted.
• EventID: Contains the event ID that you would look up online to figure out what event transpired.
• TimeCreated: A timestamp for when the event was generated.
• EventRecordID: The ID of the record, which helps you figure out the ordering of the generated records.

