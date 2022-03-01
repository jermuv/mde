# MDE
a
b
c
# Links

1
2
3


# KQL tips

4
5


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

## Basic hunting

## other