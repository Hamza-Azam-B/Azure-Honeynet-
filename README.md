Azure Honeynet: Simulating Real-World Cyber Attacks
Cloud Honeynet / SOC Project
📘 Introduction

This project demonstrates my experience building a cloud-based honeynet in Microsoft Azure to observe and analyze real-world cyber attacks. By intentionally exposing virtual machines to the internet, I collected valuable security telemetry that was ingested into Microsoft Sentinel for threat detection, visualization, and log analysis.

This hands-on project strengthened my skills in:

Azure cloud architecture

Security operations (SOC)

Kusto Query Language (KQL)

Incident monitoring and detection

Threat intelligence enrichment

Sentinel Workbooks & Watchlists

🎯 Objective

The primary objective was to deploy vulnerable cloud assets to observe:

Global attack patterns

Brute-force authentication attempts

Malicious network flows

RDP/SMB/SSH exploit attempts

Real-time threat activity targeting exposed Azure VMs

This allowed me to visualize global attacker activity and practice real SOC-style log investigations using Azure Sentinel.

🛠 Technologies & Azure Components Used
☁️ Azure Cloud Components

Azure Virtual Machines (Windows & Linux)

Azure Virtual Network (VNet)

Network Security Groups (NSGs)

Log Analytics Workspace (LAW)

Azure Storage Account

Azure Key Vault

Microsoft Sentinel (SIEM)

Microsoft Defender for Cloud

🔍 Monitoring & Security Tools

Windows Security Event Logs

Linux Syslog

NSG Flow Logs

Sentinel Data Connectors

Watchlists + GeoIP database

Sentinel Workbooks (Attack Map)

PowerShell

Azure CLI

📚 Security Frameworks Referenced

NIST SP 800-53 Rev. 5 – Cloud Security Controls

NIST SP 800-61 Rev. 2 – Incident Handling

🧪 Methodology Overview
1️⃣ Deploying the Honeynet

Deployed multiple Azure Virtual Machines with intentionally open NSG rules to attract attackers.

2️⃣ Enabling Logging

Sent logs from Windows, Linux, and NSGs into a Log Analytics Workspace.

3️⃣ Connecting Microsoft Sentinel

Sentinel was configured to ingest data, run analytics rules, and visualize real-time attacker activity.

4️⃣ GeoIP Enrichment

A large GeoIP watchlist (54k+ rows) was imported into Sentinel, allowing IP-to-country mapping.

5️⃣ KQL Log Analysis

Used KQL to:

Identify failed logons

Detect SSH/RDP brute-force attempts

Map inbound attacker IP addresses

Build attack visualizations

🌍 Global Attack Map (Sentinel Workbook)

Below is the attack map generated directly from my Azure honeynet data. It visualizes all malicious activity targeting my exposed VMs.

📸 Screenshot of My Actual Attack Map

(Stored from your uploaded image — include this in your repo under /images/attack-map.png)

![Global Attack Map](./images/attack-map.png)


This map is generated from failed authentication attempts (Windows 4625 events, Linux Syslog failures) enriched with GeoIP latitude and longitude data.

🌐 Attack Map Interpretation

Your map shows:

🔴 High-volume attacks

Large red bubble centered over Europe, indicating thousands of attempts from this region.

🟡 Medium-volume attacks

Yellow clusters originating from Asia, including Japan, the Philippines, and Indonesia.

🟢 Widespread low-volume attempts

Smaller green markers across North America, Africa, and Southeast Asia.

Each bubble represents:

Size → Number of attacks

Color → Severity / volume level

📊 Top Attacker Locations (Extracted from the Map)
Location	Approx. Count
Eibar (Spain)	3.9k
Manila (Philippines)	2.39k
United States	1.71k
China	1.18k
Swelledam (South Africa)	992
Lucknow (India)	381
Cianjur (Indonesia)	226
United States (Secondary Source)	215
Osaka (Japan)	169

Your honeynet attracted attacks from all over the globe — across four continents.

📈 KQL Queries Used for Log Analysis
🔹 1. Failed Windows Logons
SecurityEvent
| where EventID == 4625
| project TimeGenerated, Account, IpAddress, Activity

🔹 2. SSH Brute Force Attempts (Linux Syslog)
Syslog
| where Facility == "authpriv"
| where SyslogMessage contains "Failed"
| project TimeGenerated, HostName, ProcessName, SyslogMessage

🔹 3. GeoIP Enriched Events (Used for Attack Map)
let GeoIP = _GetWatchlist("geoip");
SecurityEvent
| where EventID == 4625
| evaluate ipv4_lookup(GeoIP, IpAddress, network)
| summarize Count = count() by Country, Latitude, Longitude
| order by Count desc

🧠 Conclusion

This project successfully demonstrated how exposed cloud resources are targeted globally, often within minutes of deployment. Using Microsoft Sentinel, I was able to:

Visualize global attack origins

Analyze adversary behavior

Correlate logs using KQL

Build an interactive attack map

Extract meaningful insights from real cyber attack data

This honeynet project strengthened my practical skills in:

Cloud Security

Security Operations (SOC)

Log Parsing & KQL

Sentinel Configuration

Threat Analysis

GeoIP Enrichment

🎉 If you'd like, I can add:

✅ Shields.io badges (Azure, Sentinel, SOC, KQL)
✅ A repository structure section
✅ Instructions for reproducing the attack map
✅ A professional project banner for GitHub
✅ Step-by-step setup instructions

Just tell me — I can build the full repo structure for you.
