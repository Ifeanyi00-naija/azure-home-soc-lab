# azure-home-soc-lab
Home SOC lab in Azure with Microsoft Sentinel, honeypot VM, and real-world attack analysis.


# Home SOC Lab in Azure – Honeypot with Microsoft Sentinel

This project demonstrates the setup of a basic **Security Operations Center (SOC)** environment in **Microsoft Azure**, simulating real-world attack scenarios using a public-facing honeypot virtual machine (VM), and leveraging **Microsoft Sentinel** for monitoring, analytics, and threat detection.

---

## Project Overview

- Deployed a Windows-based Virtual Machine (VM) in Azure and exposed it to the internet to act as a **honeypot**.
- Collected logs using **Azure Log Analytics Workspace**.
- Integrated the logs with **Microsoft Sentinel** for real-time monitoring and security analytics.
- Queried and visualized brute-force attack data using **Kusto Query Language (KQL)**.
- Built a **custom attack map dashboard** to geolocate and track hacker activity in real time.

---

## Tools & Technologies

| Tool | Description |
|------|-------------|
| Microsoft Azure | Cloud platform used to deploy and manage virtual infrastructure |
| Azure Virtual Machine | Simulated endpoint used as a honeypot |
| Log Analytics Workspace | Central repository for collected logs |
| Microsoft Sentinel | Cloud-native SIEM for threat detection and analytics |
| Kusto Query Language (KQL) | Used to run queries on log data |
| Azure Dashboard | Built custom visualizations for attack tracking |

---

## Key Steps

### 1. Create Free Azure Account
- Set up a free-tier subscription on [azure.com](https://azure.microsoft.com/).

### 2. Deploy & Configure a VM
- Created a Windows Server VM.
- Opened RDP port to allow public access and attract brute-force attempts.

### 3. Configure Log Analytics Workspace
- Created a workspace and linked it to the VM to collect logs such as:
  - Security Events
  - Sign-in attempts
  - Network access

### 4. Set Up Microsoft Sentinel
- Enabled Microsoft Sentinel on the workspace.
- Connected data sources and enabled built-in analytics rules.

### 5. Analyze & Visualize Attacks
- Queried failed login attempts:
  ```kql
  SecurityEvent
  | where EventID == 4625
  | summarize count() by Account, IPAddress, bin(TimeGenerated, 1h)
  (anlyze different generated times to see just how fast attckers comafetr a system once opened up to the public)
