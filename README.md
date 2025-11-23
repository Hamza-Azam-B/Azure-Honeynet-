Honeynet: Simulating Real World Cyber Attacks

<img width="1044" height="596" alt="Screenshot 2025-11-22 at 10 51 52 PM" src="https://github.com/user-attachments/assets/8344233a-f9b3-42f4-9c5d-53e4a7eafe2b" />

Cloud Honeynet / SOC Project
 Introduction

This project demonstrates my experience building a cloud-based honeynet in Microsoft Azure to observe and analyze real world cyber attacks. By intentionally exposing virtual machines to the internet, I collected valuable security data that was depoisted into Microsoft Sentinel for threat detection, visualization, and log analysis.

This hands-on project strengthened my skills in:

Azure cloud architecture
Security operations (SOC)
Kusto Query Language (KQL)
Incident monitoring and detection
Sentinel Workbooks & Watchlists

 Objective

Through this honeynet project, I was able to analyze global attack patterns. Adtionally, I was able to document widely dispersed brute-force authentication attempts, malicious network flows, RDP, and SSH exploit attempts against my exposed Azure SOC virtual machine. These real time attacks have given me a foundation into how threat actors function on the open internet. Collecting this data in Azure Sentinel allowed me to visualize attacker activity worldwide and conduct realistic investigations using enriched logs and KQL queries.



🛠 Technologies & Azure Components Used

Azure Virtual Machine (Windows)
Azure Virtual Network (VNet)
Network Security Groups (NSGs)
Log Analytics Workspace (LAW)
Azure Storage Account
Azure Key Vault
Microsoft Sentinel (SIEM)
Microsoft Defender for Cloud
Windows Security Event Logs
Linux Syslog
NSG Flow Logs
Sentinel Data Connectors
Watchlists + GeoIP database
Sentinel Workbooks (Attack Map)


Methodology Overview
Honeynet setup: I started with the deployment of several virtual machines in Azure that were deliberately vulnerable, putting them online to mimic the insecure environment of the real world and entice global hackers.
Monitoring and Analysis: Azure was set up to ingest logs from the following: Windows Security Events, Linux Syslog, and NSG flow logs to a Log Analytics Workspace. Microsoft Sentinel was used to visualize the attacks, creating an interactive global attack map and querying the collected data using KQL.
Observation of security metrics: I followed the environment for a period of 24 hours, observing key security metrics such as failed logons, brute-force attempts, and malicious inbound traffic. In this way, I came to understand just how rapidly and with what intensity exposed cloud systems are attacked.
Log investigation and enrichment: Imported large GeoIP watchlist into Sentinel to enrich attacker IP addresses with geographic data, enabling me to map the origin of the attacks and further analyze global threat patterns.
SOC Attack Analysis: With the use of KQL, I have investigated authentication failures, network traffic anomalies, and attacker behavior, emulating what a real Security Operations Center analyst might do while responding to attacks via the cloud.

Build attack visualizations

 Global Attack Map (Sentinel Workbook)

Below is the attack map generated directly from my Azure honeynet data. It visualizes all malicious activity targeting my exposed VMs.

📸 Screenshot of My Actual Attack Map

(Stored from your uploaded image — include this in your repo under /images/attack-map.png)

![Global Attack Map](./images/attack-map.png)


This map is generated from failed authentication attempts (Windows 4625 events, Linux Syslog failures) enriched with GeoIP latitude and longitude data.

🌐 Attack Map Interpretation

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


