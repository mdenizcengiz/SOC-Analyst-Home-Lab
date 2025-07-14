# SOC-Analyst-Home-Lab

### Lab Architecture and Overview
This hands-on cybersecurity lab simulates the core responsibilities of a SOC Analyst by walking through the process of deploying a honeypot in Microsoft Azure, capturing real-time attack data, and analyzing it using Microsoft Sentinel. I set up a vulnerable virtual machine to attract brute-force login attempts, forwarded security logs to a Log Analytics Workspace, and used Kusto Query Language (KQL) to investigate failed login events. I then enriched the logs with geolocation data and created a visual attack map using Sentinel Workbooks to identify and display the origin of malicious activity. This lab reinforced key SOC skills such as threat detection, log correlation, SIEM usage, and incident investigation.

### Honeypot Deployment, Log Analysis, and Threat Detection in Azure Sentinel

📌 Project Summary (SOC Analyst Focus):
- Deployed a honeypot using an Azure Windows 10 Virtual Machine to simulate brute-force attack scenarios in a controlled environment.

- Configured network and system settings (e.g., open inbound rules, disabled firewall) to intentionally expose the VM and attract attacker behavior.

- Collected and forwarded security logs to Azure Log Analytics Workspace for centralized visibility.

- Integrated Microsoft Sentinel with the workspace to act as the SIEM platform for alerting and investigation.

- Queried and analyzed logs using Kusto Query Language (KQL) to identify unauthorized login attempts (Event ID 4625).

- Enriched logs with geolocation data via Sentinel Watchlists to determine the origin of attacks based on IP addresses.

- Built a real-time attack map using Sentinel Workbooks to visualize attack patterns and source regions.

- Developed hands-on skills in threat detection, log enrichment, and security event investigation.

- Strengthened understanding of SIEM architecture, incident response workflow, and the use of industry-standard tools (Azure, KQL, Sentinel).

---




