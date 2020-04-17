# Windows Event Logs

Each log is stored in a separate file in paths specified within registry key

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog.
```

## Windows XP, Windows Server 2003, and prior operating systems

The default event log paths are

### Application

```text
%SYSTEMROOT%\System32\Config\AppEvent.Evt
```

### System

```text
%SYSTEMROOT%\System32\Config\SysEvent.Evt
```

### Security

```text
%SYSTEMROOT%\System32\Config\SecEvent.Evt
```

## Windows Vista and above

EVT files were scrapped for a new XML-based format using the extension .evtx. The default paths were as below:

### Application

```text
%SYSTEMROOT%\System32\Winevt\Logs\Application.evtx
```

### System

```text
%SYSTEMROOT%\System32\Winevt\Logs\System.evtx
```

### Security

```text
%SYSTEMROOT%\System32\Winevt\Logs\Security.evtx
```

![An example of event log](../.gitbook/assets/image%20%2810%29.png)

User Name The account used to log on. 

Domain The domain associated with the user name. If the user name is a local account, this field will contain the system’s host name. 

Logon ID A unique session identifier. You can use this value as a search term or filter to find all event log entries associated with this specific logon session. 

Logon Type A code referencing the type of logon initiated by the user. The following table provides further detail on the Logon Type field and its possible values:

![](../.gitbook/assets/image%20%2817%29.png)

