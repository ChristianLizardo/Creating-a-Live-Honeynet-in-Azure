# Creating-a-Live-Honeynet-in-Azure

In this project, I create a small-scale honeynet using Microsoft Azure to attract real-world traffic from attackers worldwide. The primary goal is to demonstrate best practices in security, incident response strategies, and the impact of hardening an environment. To achieve this, we intentionally deploy virtual machines exposed to the public internet to lure attackers into the setup. After capturing attack data, we ingest log sources into Log Analytics Workspace and utilize Microsoft Sentinel to generate attack maps, alerts, and incidents. This allows us to showcase metrics comparing the state of the environment before and after implementing hardening measures based on incidents captured over a 24-hour period.

# Environments and Technology Used 

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel
- Microsoft Defender for Cloud

#  Architecture before Hardening 

During the initial phase of the project, resources were intentionally set up to be exposed to public internet traffic. Virtual Machines were configured with minimal restrictions, leaving both their Network Security Groups (NSGs) and firewalls open to allow access from any source. Similarly, other components, such as storage accounts and databases, were accessible via public endpoints without the added protection of Private Endpoints. This setup was maintained for 24 hours to monitor activity and gather data for the attack maps referenced earlier.

This attack map highlights the volume of incidents resulting from an open Network Security Group (NSG) configuration.

Insert Image

This attack map highlights the incidents for syslog authentication failures experienced by the Linux server.

Insert Image

This attack map displays RDP and SMB failure attempts targeting the Windows machine

Insert Image

This attack map showcases failures against the MSSQL server.

Insert Image

# After Hardening Measures and Security Control 

In the "AFTER" stage of the project, I implemented targeted hardening measures and security controls based on the incidents observed during the initial 24-hour capture. These enhancements significantly improved the environment's resilience against attacks. The key improvements included:

Network Security Groups (NSGs): The NSGs were fortified by restricting access exclusively to my public IP address, effectively blocking all other traffic through the newly configured rules.

Built-in Firewalls: The built-in firewalls on the virtual machines were configured to deny access to unauthorized users, providing an additional layer of defense.

Private Endpoints: Public endpoints for Azure resources, such as storage accounts and databases, were replaced with Private Endpoints. This change ensured that these resources could only be accessed within the virtual network, safeguarding sensitive data from external exposure.

These measures collectively reduced vulnerabilities and improved the overall security posture of the environment.

# Attacks maps after Hardening and Security Controls

All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

|     Metric      |          Count        |
|---------------|--------------------------|
| SecurityEvent ( Windows VM) | 4358 |
| Syslog ( Linux VM ) | 2345 |
| SecurityAlert( Microsoft Defender for Cloud ) | 6 |
| SecurityIncident ( Sentinel Incidents)   | 73 |
| NSG Inbound Malicious  Flows Ahead | 103 |
