# Windows Event Logs

Each log is stored in a separate file in paths specified within registry key
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog. 
```
## Windows XP, Windows Server 2003, and prior operating systems

The default event log paths are
### Application 
```
%SYSTEMROOT%\System32\Config\AppEvent.Evt
```
### System 
```
%SYSTEMROOT%\System32\Config\SysEvent.Evt
```
### Security 
```
%SYSTEMROOT%\System32\Config\SecEvent.Evt
```
## Windows Vista and above
EVT files were scrapped for a new XML-based format using the extension .evtx. The default paths were as below:

### Application 
```
%SYSTEMROOT%\System32\Winevt\Logs\Application.evtx
```
### System 
```
%SYSTEMROOT%\System32\Winevt\Logs\System.evtx
```
### Security 
```
%SYSTEMROOT%\System32\Winevt\Logs\Security.evtx
```
