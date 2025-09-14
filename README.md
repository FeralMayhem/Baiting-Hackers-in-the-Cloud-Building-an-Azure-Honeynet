# Baiting-Hackers-in-the-Cloud-Building-an-Azure-Honeynet
Azure Honeynet Project

![Untitled](https://github.com/user-attachments/assets/6a006964-3997-44ee-a11a-e241816960a4)

## Introduction

For this project, I set up a miniature "digital trap" — known as a honeynet — in Microsoft Azure. I connected all kinds of resources to a central logging system (a Log Analytics workspace) and used Microsoft Sentinel to detect attacks, map them visually, and generate security alerts.

To really see the impact, I first measured what the landscape looked like for one hour while the system was intentionally left vulnerable. Then, I stepped in to lock things down with stronger security controls. Finally, I measured everything again for another hour to see how much of a difference those changes made.

Here’s a side-by-side look at the results, including key security metrics like:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- NTANetAnalytics (Malicious NSG Flows allowed into the honeynet)

## Architecture Before Hardening / Security Controls

![Before-Hardening](https://github.com/user-attachments/assets/100f499a-cb84-4bd2-96a2-26463bdefd60)

## Architecture After Hardening / Security Controls

![After-Hardening](https://github.com/user-attachments/assets/37916792-a0cb-4570-8aca-82bac0a5927c)

The architecture of the honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (1 Windows 10, 1 Linux - Ubuntu)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account (Blob Storage)
- Microsoft Sentinel/Defender

For the "BEFORE" metrics, the environment was intentionally left exposed. All resources were publicly accessible from the internet, with open Network Security Groups and disabled firewalls on the Virtual Machines. No private endpoints were used, and everything was visible and reachable online.

For the "AFTER" metrics, I locked things down. We hardened the Network Security Groups to block all traffic except from my trusted admin device, enabled the built-in firewalls on each resource, and implemented Private Endpoints to ensure all communication stayed within our secured private network.

## Attack Maps Before Hardening / Security Controls
<img width="2172" height="427" alt="Linux" src="https://github.com/user-attachments/assets/834ede44-3e9d-471b-ae84-57399b4e4902" />

<img width="2141" height="430" alt="NSG" src="https://github.com/user-attachments/assets/014ac05b-dbf4-4de3-9678-6f47395ba24f" />

<img width="2146" height="434" alt="Windows" src="https://github.com/user-attachments/assets/d23482ea-4bc7-4ade-805a-deeb0dd51412" />


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for one hour:

Start Time: 14/09/2025, 19:59 PM BST
Stop Time: 14/09/2025, 20:59 PM BST


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows)  | 469
| Syslog    (Linux VM)     | 1719
| Sentinel Incidents       | 117
| NTANetAnalytics          | 1390

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for a one hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for an hour, but after we have applied security controls:
Start Time: 14/09/2025, 22:30 PM BST
Stop Time: 14/09/2025, 23:30 PM BST

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 
| Syslog                   | 25
| SecurityIncident         | 0
| NTANetAnalytics          | 0
