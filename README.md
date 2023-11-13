# Building a SOC + Honeynet in Azure (Live Traffic)


## Introduction

In this project,  I established a compact honeynet within Azure, funneling log data from multiple sources into a Log Analytics workspace. This data was then processed by Microsoft Sentinel to create attack visuals, generate alerts, and initiate incidents. The project involved monitoring security metrics in a vulnerable setup for a day, implementing security enhancements, monitoring for another day, and then presenting the comparative results. The metrics under consideration include:

- Windows Event Logs (SecurityEvent)
- Linux Event Logs (Syslog)
- Alerts generated in Log Analytics (SecurityAlert)
- Incidents initiated by Sentinel (SecurityIncident)
- Unwanted traffic allowed in our honeynet (AzureNetworkAnalytics_CL)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The Azure honeynet architecture comprised:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

Initially, all resources were deployed and made accessible online. The VMs had their NSGs and built-in firewalls completely unrestrictive, and other resources were set up with public endpoints without private endpoints.

Post-enhancements, the NSGs were fortified, allowing only my admin workstation's traffic. Simultaneously, other resources were secured using their inherent firewalls and the addition of Private Endpoints.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-09-07 17:04:29
Stop Time 2023-09-07 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-09-07 15:37
Stop Time	2023-09-07 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

Through this initiative, a honeynet was set up in Azure, with logs incorporated into a dedicated workspace. Microsoft Sentinel's capabilities were utilized to generate pertinent alerts and incidents. A notable observation was the significant drop in security events post the introduction of robust security measures.

It's pertinent to mention that an increase in legitimate user activity might have potentially resulted in a spike in security events and alerts in the subsequent 24-hour window after the security measures were enforced.
