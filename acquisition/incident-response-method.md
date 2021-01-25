# Live Data Collection

## Redline
1. Installed Redline on your system and launch the tool
2. Click the option **Create Comprehensive Collector**. Then browse to the location you would like to save the collector (preferably an USB or external hard drive).  
3. Before you save the collector, you can view and tweak the collection parameters by clicking the Edit Your Script link.
4. Use Windows Explorer to browse to the directory and then double-click on the file named **RunRedlineAudit.bat**.

## Windows

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

## Linux
