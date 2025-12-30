# Azure Sentinel Windows Honeypot

This repository demonstrates a SOC lab implementation using Microsoft Azure and Microsoft Sentinal.
A Windows VM was deployed as a Honeypot to capture failed authentication attempts. The logs are then used to visualizes attacker source IP addresses on a global map using Microsoft Sentinel.

## Project Overview

This project shows how to:

- Configure a Windows VM in Azure as a honeypot
- Enable Windows Security Event log collection (Event ID 4625)
- Extract attacker IP addresses using KQL
- Visualize failed login source IPs on a world map using Microsoft Sentinel Workbooks

## Contents

| Folder | Description |
|--------|-------------|
| `kql/` | KQL queries to extract failed login IPs |
| `workbooks/` | Workbook(s) for visual mapping |
| `setup/` | Setup and configuration instructions |
| `screenshots/` | Example screenshots of dashboards or maps |

---

## Requirements

- Azure Subscription
- Log Analytics Workspace
- Microsoft Sentinel enabled
- Windows VM with Security log collection

---

## KQL Query
------------
```
let GeoIPDB_FULL = _GetWatchlist("geoip");
let WindowsEvents = SecurityEvent;
WindowsEvents | where EventID == 4625
| order by TimeGenerated desc
| evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network)
| summarize FailureCount = count() by IpAddress, latitude, longitude, cityname, countryname
| project FailureCount, AttackerIp = IpAddress, latitude, longitude, city = cityname, country = countryname,
friendly_location = strcat(cityname, " (", countryname, ")");
```

## Workbook Query
-----------------
```

  
