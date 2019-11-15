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
