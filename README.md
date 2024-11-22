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

# Metrics before Hardening / Security Control 

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023 05-03 09:15 AM
Stop Time 2023-05-04 09:15 AM

|     Metric      |          Count        |
|---------------|--------------------------|
| SecurityEvent ( Windows VM) | 4358 |
| Syslog ( Linux VM ) | 2345 |
| SecurityAlert( Microsoft Defender for Cloud ) | 6 |
| SecurityIncident ( Sentinel Incidents)   | 73 |
| NSG Inbound Malicious  Flows Ahead | 103 |

# Metrics After Hardening / Security Control 

The following table shows the metrics we measured in our secure environment for 24 hours:
Start Time 2023-05-04 4:25 PM
Stop Time 2023-05-05 4:25 PM

|     Metric      |          Count        |
|---------------|--------------------------|
| SecurityEvent ( Windows VM) | 2364 |
| Syslog ( Linux VM ) | 24|
| SecurityAlert( Microsoft Defender for Cloud ) | 0 |
| SecurityIncident ( Sentinel Incidents)   | 0 |
| NSG Inbound Malicious  Flows Ahead | 0 |

# Utilizing NIST 800.61r2 Computer Incident Handling Guide

For each simulated attack I practiced incident responses following NIST SP 800-61 r2.

Insert Image


Each organization follows specific policies for incident response, which should guide actions during potential security events. This walkthrough demonstrates a possible approach for addressing malware detected on a workstation.

# Preparation

The lab environment was configured to collect logs into Log Analytics Workspace. Security tools such as Sentinel and Defender were set up with alert rules to monitor and respond to threats.

# Detection & Analysis

   - Malware was identified on a workstation, posing risks to the system's confidentiality, integrity, and availability.
   - The alert was assigned to a designated owner, marked as "High" severity, and set to "Active" status.
   - The primary user of the system and other affected systems were identified.
   - A comprehensive system scan using updated antivirus software pinpointed the malware.
   - The alert was verified as a valid threat ("True Positive").
   - Notifications were sent to the appropriate personnel as per communication protocols.
  
# Containment, Eradication, & Recovery

  - The infected workstation, along with any other compromised systems, was isolated from the network.
  - If malware removal was unsuccessful or system integrity was compromised, affected systems were powered down and disconnected.
  - Recovery options included restoring systems to a clean state, such as using system images or reinstalling the operating system and applications. Alternatively, 
    updated antivirus software was employed to remove the malware.
  
# Post-Incident Actions

  - Analysis revealed that an employee had downloaded a game containing malicious software.
  - Data was collected to assess the root cause, the extent of the impact, and the response effectiveness.
  - A report was prepared and shared with relevant stakeholders.
  - Corrective measures were implemented to address the root cause.
  - A lessons-learned review was conducted to improve future incident response efforts.

 # Conclusion 

 
This project involved building a small honeynet in Microsoft Azure, where log data was integrated into a Log Analytics Workspace. Microsoft Sentinel was used to generate alerts and incidents based on the collected logs. Metrics were recorded in the environment both before and after applying security controls, demonstrating a significant reduction in security events and incidents once the controls were in place, highlighting their effectiveness in enhancing the environment's protection.

It is important to consider that if the resources in the network had been actively used by regular users, the volume of security events and alerts during the 24-hour period following the implementation of security measures could have been higher.

















