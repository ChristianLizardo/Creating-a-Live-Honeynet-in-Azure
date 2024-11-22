# Creating-a-Live-Honeynet-in-Azure

In this project, I create a small-scale honeynet using Microsoft Azure to attract real-world traffic from attackers worldwide. The primary goal is to demonstrate best practices in security, incident response strategies, and the impact of hardening an environment. To achieve this, we intentionally deploy virtual machines exposed to the public internet to lure attackers into the setup. After capturing attack data, we ingest log sources into Log Analytics Workspace and utilize Microsoft Sentinel to generate attack maps, alerts, and incidents. This allows us to showcase metrics comparing the state of the environment before and after implementing hardening measures based on incidents captured over a 24-hour period.

# Environments and Technology Used 
-Azure Virtual Network (VNet)
-Azure Network Security Group (NSG)
-Virtual Machines (2x Windows, 1x Linux)
-Log Analytics Workspace with Kusto Query Language (KQL) Queries
-Azure Key Vault
-Azure Storage Account
-Microsoft Sentinel
-Microsoft Defender for Cloud
