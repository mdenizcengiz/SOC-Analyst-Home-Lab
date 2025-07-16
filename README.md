# SOC-Analyst-Home-Lab

### Lab Architecture and Overview
This hands-on cybersecurity lab simulates the core responsibilities of a SOC Analyst by walking through the process of deploying a honeypot in Microsoft Azure, capturing real-time attack data, and analyzing it using Microsoft Sentinel. I set up a vulnerable virtual machine to attract brute-force login attempts, forwarded security logs to a Log Analytics Workspace, and used Kusto Query Language (KQL) to investigate failed login events. I then enriched the logs with geolocation data and created a visual attack map using Sentinel Workbooks to identify and display the origin of malicious activity. This lab reinforced key SOC skills such as threat detection, log correlation, SIEM usage, and incident investigation.

### Honeypot Deployment, Log Analysis, and Threat Detection in Azure Sentinel

### Project Summary
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

### Steps
### 1. Create Resource Group
I created a dedicated resource group named to organize and manage all resources used in the SOC lab environment.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/2-Resource%20Group.png)


### 2.Create Virtual Network
I created a virtual network within the resource group to simulate an enterprise network environment. This VNet provides the underlying infrastructure for deploying the honeypot and other security resources. supporting secure traffic routing and monitoring within the lab.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/1-Create%20Virtual%20Network.png)

### 3. Setup VM
I deployed a Windows virtual machine within the resource group and connected it to the virtual network. This VM acts as a honeypot to attract and log unauthorized access attempts. It uses a public IP address for external accessibility, simulating a vulnerable endpoint in a real-world environment.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/3-Setup%20Virtual%20Machine.png)

### 4. Disable Firewall in VM
After deploying the honeypot VM, I disabled Windows Defender Firewall to simulate a vulnerable endpoint and allow unrestricted traffic into the machine for testing purposes.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/4-Disable%20Firewall%20in%20VM.png)

### 5. Configure Network Security Group (NSG)
I created a high-priority rule in the NSG to allow all inbound traffic from any source and port. This exposes the honeypot VM to potential threats and enables log generation for failed login attempts.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/5-Network%20Security%20Group.png)

### 6. Simulate Failed Login Attempts
After RDP access to the honeypot VM, I triggered multiple failed login attempts using invalid usernames. These attempts were logged as Event ID 4625, which indicates failed authentication.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/6-Unsuccessful%20logon%20attempts.png)

### 7. Create Log Analytics Workspace
To centralize log collection, I created a Log Analytics Workspace (LAW). This workspace acts as a repository for Windows event logs forwarded from the honeypot.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/7-%20Create%20Log%20Analytics%20Workspace.png)

### 8. Create Sentinel SIEM
I connected Microsoft Sentinel to the Log Analytics Workspace. Sentinel acts as the SIEM platform to analyze, correlate, and visualize the incoming security data.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/8-Create%20Microsoft%20Sentinel%20SIEM.png)

### 9. Install Security Events Connector
I configured the "Windows Security Events via AMA" data connector in Sentinel to collect login-related events from the honeypot.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/9-install%20security%20events.png)

### 10. Install Azure Monitoring Extension
On the honeypot VM, I installed the Azure Monitor Agent extension to enable telemetry collection and log forwarding to Azure Monitor.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/10-Extension%20for%20security%20log%20collecter.png)

### 12. Create Data Collection Rule
I created a Data Collection Rule (DCR) to define how logs from the VM are collected and where they are sent. This rule ensures only relevant Windows Event Logs are forwarded.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/11-Create%20data%20collection%20rules%20for%20VM.png)

### 13. Verify Log Collection (Initial Logs)
After setup, I verified that logs were flowing into the workspace by querying all SecurityEvent logs in the Log Analytics interface.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/12-%20First%20Log.png)

### 14. Filter Logs for Event ID 4625 (Failed Logins)
Using KQL, I filtered logs to show only failed login attempts (Event ID 4625), which originated from my earlier brute-force simulation on the VM.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/13-Event%20ID%204625.png)

### 15. Enriched Logs with GeoIP Data
Using a custom watchlist and the ipv4_lookup() function in KQL, I enriched failed login logs with geographic information such as city, country, latitude, and longitude. This enabled better threat attribution and visibility into attacker origins.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/14-With%20GEO%20IP.png)

### 16. Created Sentinel Watchlist with GeoIP Data
I imported a CSV file into Microsoft Sentinel as a watchlist. This watchlist contains over 55,000 IP-to-location mappings used to correlate IPs in login logs with geolocation data.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/16-Create%20a%20workbook%20for%20geo%20ip.png)

### 17. Created a Sentinel Workbook for GeoIP Analysis
I created a new workbook in Microsoft Sentinel to visualize security data. This served as the base structure for building the Windows VM Attack Map.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/16-Create%20a%20workbook%20for%20geo%20ip.png)

### 18. Visualized Attacks on a Global Map (Attack Map)
Using the enriched data and KQL visualizations in Sentinel, I built an interactive attack map that displays attack origin locations based on IP geolocation. This helped identify hotspots and common sources of brute-force attempts.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/18-Windows%20VM%20Attack%20Map.png)

### 19. Configured Custom Analytics Rules in Sentinel
I configured multiple custom detection rules in Sentinel, including alerts for brute force attacks, privilege escalation, and rare RDP connections. These rules are aligned with MITRE ATT&CK tactics and support proactive threat detection.

![image alt](https://github.com/mdenizcengiz/SOC-Analyst-Home-Lab/blob/84c85619a8c3d01effd6ea211378ffc6da116e82/screenshots/17-Custom%20Incident%20rules.png)


