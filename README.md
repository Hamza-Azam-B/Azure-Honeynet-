## Honeynet: Simulating Real Time Cyber Attacks

<img width="1044" height="596" alt="soc-lab" src="https://github.com/user-attachments/assets/62510417-085f-4296-a466-fb869962348f" />

 ## Introduction

This project demonstrates my experience building a cloud-based honeynet in Microsoft Azure to observe and analyze real world cyber attacks. By intentionally exposing my virtual machine to the internet, I collected valuable security data that was depoisted into Microsoft Sentinel for threat detection, visualization, and log analysis.

## This hands-on project strengthened my skills in:

 Azure cloud architecture
 Security operations (SOC)
 Kusto Query Language (KQL)
 Incident monitoring and detection
 Sentinel Workbooks & Watchlists

 ## Objective

Through this honeynet project, I was able to analyze global attack patterns. Adtionally, I was able to document widely dispersed brute-force authentication attempts, malicious network flows, RDP, and SSH exploit attempts against my exposed Azure SOC virtual machine. These real time attacks have given me a foundation into how threat actors function on the open internet. Collecting this data in Azure Sentinel allowed me to visualize attacker activity worldwide and conduct realistic investigations using enriched logs and KQL queries.



 ## Technologies & Azure Components Used

- Azure Virtual Machine (Windows)
- Azure Virtual Network (VNet)
- Network Security Groups (NSGs)
- Log Analytics Workspace (LAW)
- Azure Storage Account
- Azure Key Vault
- Microsoft Sentinel (SIEM)
- Microsoft Defender for Cloud
- Windows Security Event Logs
- Sentinel Data Connectors
- Watchlists + GeoIP database
- Sentinel Workbooks (Attack Map)


## Methodology Overview

Honeynet setup:
- I started with the deployment of my windows 11 virtual machine in Azure that were deliberately vulnerable, putting them online to mimic the insecure environment of the real world and entice global hackers.

Monitoring and Analysis: 
- Azure was set up to ingest logs from the following: Windows Security Events, Linux Syslog, and NSG flow logs to a Log Analytics Workspace. Microsoft Sentinel was used to visualize the attacks, creating an interactive global attack map and querying the collected data using KQL.

Observation of security metrics:
- I followed the environment for a period of 24 hours, observing key security metrics such as failed logons, brute-force attempts, and malicious inbound traffic. In this way, I came to understand just how rapidly and with what intensity exposed cloud systems are attacked.

Log investigation and enrichment: 
- Imported large GeoIP watchlist into Sentinel to enrich attacker IP addresses with geographic data, enabling me to map the origin of the attacks and further analyze global threat patterns.

SOC Attack Analysis: 
- With the use of KQL, I have investigated authentication failures, network traffic anomalies, and attacker behavior, emulating what a real Security Operations Center analyst might do while responding to attacks via the cloud.


## Global Attack Map (Sentinel Workbook)

Below is the attack map generated directly from my Azure honeynet data. It visualizes all malicious activity targeting my exposed VMs.

<img width="1234" height="712" alt="Screenshot 2025-11-22 at 10 18 59 PM" src="https://github.com/user-attachments/assets/20fbbd20-8d3e-4864-b835-cdee14c8aea7" />


This map is generated from failed authentication attempts (Windows 4625 events, Linux Syslog failures) enriched with GeoIP latitude and longitude data.

 ## Attack Map Interpretation

 High-volume attacks

- Large red bubble centered over Europe, indicating thousands of attempts from this region.

 Medium-volume attacks

- Yellow clusters originating from Asia, including Japan, the Philippines, and Indonesia.

 Widespread low-volume attempts

- Smaller green markers across North America, Africa, and Southeast Asia.

Each bubble represents:

Size → Number of attacks

Color → Severity 

## Top Attacker Locations


<img width="359" height="362" alt="Screenshot 2025-11-23 at 12 40 43 AM" src="https://github.com/user-attachments/assets/dec373b6-db08-4c0a-9f3a-ae20ece35240" />




 ## KQL Query used to determine TimeGenerarted, Actvity IPAdress, countryname, cityname
 

<img width="1434" height="674" alt="Screenshot 2025-11-23 at 1 55 27 AM" src="https://github.com/user-attachments/assets/718fe863-1873-42e7-bda0-5e3ef2b25c7c" />

 ## KQL Query to find the most number of attack sources
 
 <img width="1436" height="672" alt="Screenshot 2025-11-23 at 2 06 06 AM" src="https://github.com/user-attachments/assets/d03993fd-41b1-4f36-aa80-af7e003c45f5" />

 

## GeoIP Enriched Events (Used for Attack Map)


<img width="1434" height="666" alt="Screenshot 2025-11-23 at 2 29 00 AM" src="https://github.com/user-attachments/assets/ac62639b-a2a8-4337-ad48-d47bb356b6e7" />



## Conclusion

This project successfully demonstrated how exposed cloud resources are targeted globally, often within minutes of deployment. Using Microsoft Sentinel, I was able to:

- Visualize global attack origins
- Analyze adversary behavior
- Correlate logs using KQL
- Build an interactive attack map
- Extract meaningful insights from real cyber attack data


Through this honeynet, I also strengthened my practical skills in several key areas, including:

- Cloud Security
- Security Operations (SOC)
- Log Parsing & KQL
- Sentinel Configuration
- Threat Analysis
- GeoIP Enrichment



