# Live Data Collection

## Redline

1. Installed Redline on your system and launch the tool
2. Click the option **Create Comprehensive Collector**. Then browse to the location you would like to save the collector \(preferably an USB or external hard drive\).  
3. Before you save the collector, you can view and tweak the collection parameters by clicking the Edit Your Script link.
4. Use Windows Explorer to browse to the directory and then double-click on the file named **RunRedlineAudit.bat**.

## KAPE

Update KAPE with the powershell script with the administrator command prompt:

```text
powershell -ep Bypass .\Get-KAPEUpdate.ps1
```

![](../.gitbook/assets/image%20%2816%29.png)

Manually replace the Targets and Modules folders with the one inside KapeFiles-master

![](../.gitbook/assets/image%20%2819%29.png)

Run command

In order to run the Modules, place all the executables under KAPE\Modules\bin

![](../.gitbook/assets/image%20%2844%29.png)

Note: KAPE\Modules\bin\regripper should contains p2x5124.dll

![](../.gitbook/assets/image%20%2820%29.png)

## bulk\_extractor



## Windows

Below list out a list of information we need to collection during a live response on Windows PC.

| Data to be collected | Command /Tools |
| :--- | :--- |
| System date and time | date and time |
| Time zone / Installed software / General system information /OS version/ Uptime /File system information | systeminfo |
| User accounts | net user |
| Groups | net group |
| Network interfaces | ipconfg/all |
| Routing table | route print |
| ARP table | arp -a |
| DNS cache | ipconfig/displaydns |
| Network connections | netstat -abn |
| List of services and tasks | Microsoft autoruns |
| Loaded drivers | NirSoft DriverView |
| Open files and handles | NirSoft OpenedFilesView |
| Running processes | Microsoft pslist |
| Registry \(config data\) | Microsoft logparser |
| Event logs \(login history\) | Microsoft logparser |
| File system listing | Microsoft logparser |
| LR output checksum computation | PC-Tools.net md5sums or hashutils |

## Linux

Below list out a list of information we need to collection during a live response on Linux PC.

