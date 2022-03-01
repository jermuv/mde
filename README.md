# MDE

# Links

# KQL tips

## Basic search

Network stuff:
```
// show all network ports used
DeviceNetworkEvents
| where DeviceName == "tools.contoso.lab"
| project RemotePort
| distinct RemotePort
| order by RemotePort asc

//show only http/https
DeviceNetworkEvents
| where DeviceName == "tools.contoso.lab"
| where RemotePort == 80 or RemotePort == 443

//show only http/https events for nonsystem accounts
DeviceNetworkEvents
| where DeviceName == "tools.contoso.lab"
| where RemotePort == 80 or RemotePort == 443
| where InitiatingProcessAccountName != "system" and InitiatingProcessAccountName != ""

//show browsing history
DeviceNetworkEvents
| where DeviceName == "tools.contoso.lab"
| where RemotePort == 80 or RemotePort == 443
| where InitiatingProcessFileName == "msedge.exe"

//show browsing history, urls only
DeviceNetworkEvents
| where DeviceName == "tools.contoso.lab"
| where RemotePort == 80 or RemotePort == 443
| where InitiatingProcessFileName == "msedge.exe"
| project RemoteUrl
| distinct RemoteUrl
| order by RemoteUrl

```

Device Events:

```
DeviceEvents
| where DeviceName != "win-trfl5rqp5g8"
| order by Timestamp desc

// finding all event types 
DeviceEvents
| where DeviceName != "win-trfl5rqp5g8"
| project ActionType
| distinct ActionType
| order by ActionType asc

// finding event types with scheduled
DeviceEvents
| where DeviceName != "win-trfl5rqp5g8"
| where ActionType contains "Scheduled"
| project ActionType
| distinct ActionType
| order by ActionType asc

// find new scheduled tasks
DeviceEvents
| where DeviceName != "win-trfl5rqp5g8"
| where ActionType contains "ScheduledTaskCreated"

```




## Browser stuff

```
DeviceFileEvents
| where InitiatingProcessFileName in~ ("browser_broker.exe", "chrome.exe", "iexplore.exe", "firefox.exe", "outlook.exe", "msedge.exe")
| where FileName endswith ".zip"
// The FileOrigin* columns are available only on Edge and Chrome and from Windows 10 version 1703
// https://techcommunity.microsoft.com/t5/Threat-Intelligence/Hunting-tip-of-the-month-Browser-downloads/td-p/220454
| project Timestamp, DeviceName, FileName, FolderPath, FileOriginUrl, FileOriginReferrerUrl, FileOriginIP
```



## other