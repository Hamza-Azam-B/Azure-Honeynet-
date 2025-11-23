# Azure-Honeynet-
This project involves deploying a cloud-based honeynet in Azure to attract and analyze cyber attacks. By exposing vulnerable systems, I observed attacker behavior, collected telemetry, and evaluated security hardening measures. The project demonstrates the value of honeynets for threat intelligence and incident response.
📌 Part 1 — Setup Azure Subscription

Create a free Azure subscription:
https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account

If Azure does not allow you to create a free account, you may:

Create a paid subscription (be careful to shut down/delete resources to avoid charges), or

Join the Cyber Range (flat fee & everything is set up for you):
https://skool.com/cyber-range

Once the subscription is active, sign in:
https://portal.azure.com

📌 Part 2 — Create the Honeypot (Azure Virtual Machine)
1. Create the Windows 10 VM

Go to Azure Portal → Virtual Machines

Click Create

OS: Windows 10

VM Size: choose small/cheap if running in your own subscription

Record the username and password

2. Allow all inbound traffic

Open your VM’s Network Security Group (NSG)

Create an Inbound Rule:

Source: Any

Port: Any

Protocol: Any

Action: Allow

Priority: Low number (100–200)

(This intentionally exposes the VM for attack — DO NOT do this in production.)

3. Disable Windows Firewall

Inside the VM:

Start → wf.msc → Windows Firewall Properties → Turn Off for all profiles

📌 Part 3 — Logging Into the VM & Inspecting Logs
1. Generate authentication failures

Fail login 3 times using a fake username (ex: employee).

2. Successfully log in
3. Inspect the Windows Security Logs

Inside the VM:

Open Event Viewer

Navigate: Windows Logs → Security

Find failed login events: Event ID 4625

📌 Part 4 — Log Forwarding + KQL
1. Create a Log Analytics Workspace (LAW)

Azure Portal → Log Analytics Workspaces → Create

2. Create and connect Microsoft Sentinel

Open the LAW

Select Microsoft Sentinel → Create

3. Configure Log Collection (AMA)

Go to Sentinel → Content Hub → Data connectors

Configure Windows Security Events via AMA

Create the DCR (Data Collection Rule)

4. Run a KQL query

In Logs (either LAW or Sentinel):
