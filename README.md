# Building a Security Operations Center and Honeynet Project in Azure w/ Live Traffic

![Azure Project](https://github.com/letumnu/HoneyNet/assets/23455567/541459b9-17be-44b3-8d84-c3cd67f38dd7)

## Introduction

In this project, I built a small honeynet in Azure and ingested logs from various sources into a configured Log Analytics Worskpace. Microsoft Sentinel then used those aggregate logs to build attack maps, trigger various alerts and created incidents. I unsecured the environment for 24 hours and measured the metrics. I then applied some security controls to harden the environment and measured the metrics for another 24 hours with the results below. These are the following metrics that will be shown:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Azure Architecture "PRE" Hardening Implementation/Security Controls
![Azure Project2](https://github.com/letumnu/HoneyNet/assets/23455567/9fcb50bd-0605-49ad-9cd4-41285a63ce61)



## Azure Architecture "POST" Hardening Implementation/Security Controls
![Azure Project3](https://github.com/letumnu/HoneyNet/assets/23455567/dbfd7e53-85f3-443b-b279-cf5763ba3574)


The architecture of the mini honeynet in Azure consists of:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

The "PRE" metrics indicate that all resources were originally deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls open, and all other resources are deployed with public endpoints were made visible to the Internet.

The "POST" metrics indicate that Network Security Groups were hardened by blocking ALL traffic with the exception of the admin workstation. All other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
[NSG Allowed Inbound Malicious Flows]![NSG Flow Logs](https://github.com/letumnu/HoneyNet/assets/23455567/c9f93049-d9c1-42e1-85c6-302d98eab222)
<br>
[Linux Syslog Auth Failures]![Linux Fail](https://github.com/letumnu/HoneyNet/assets/23455567/62321990-9b57-4167-aae9-320d48f1a112)
<br>
[Windows RDP/SMB Auth Failures]![Windows RDp](https://github.com/letumnu/HoneyNet/assets/23455567/a0faa21a-0bca-48a9-ac44-7a678a20df63)
<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:<br>
Start Time 2023-05-23 12:51:41<br>
Stop Time 2023-05-24 12:51:41

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 843

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was successfull employed to trigger alerts and create incidents from the ingested logs. Furthermore, the aforementioned metrics were measured in the insecure environment before and after securirty controls were applied. Its remarkable that the number of security related events and incidents were drasitcally reduced after subsequent application of security controls; demonstrating their effectiveness. This also goes to show that if resources were actively utilized bby regular users, there's a higher probability that more security events and alerts may have been generated with the 24-hour period after implementing secuirty controls.
