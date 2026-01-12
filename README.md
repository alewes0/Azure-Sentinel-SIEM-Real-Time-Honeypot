# Azure Sentinel (SIEM) & Real-Time Honeypot

## Introduction
This project demonstrates the setup of a cloud-native **SIEM (Microsoft Sentinel)** integrated with a live virtual machine acting as a **Honeypot**. The goal was to observe, analyze, and visualize real-world RDP brute-force attacks from across the globe in real-time.

---

## Architecture & Data Flow
* **Azure Virtual Machine:** A Windows VM was deployed with its Network Security Group (NSG) intentionally misconfigured to allow all incoming traffic (RDP port 3389).
* **Custom PowerShell Script:** A script ran continuously on the VM to monitor Windows Event Viewer for failed login attempts (**Event ID 4625**).
* **API Integration:** The script sent the attacker's IP addresses to a **Geolocation API** to retrieve latitude, longitude, and country data.
* **Log Analytics Workspace:** The enriched log data was forwarded to a custom log in Azure Log Analytics for indexing.
* **Microsoft Sentinel:** Used **KQL (Kusto Query Language)** to query the logs and visualize the attack patterns on a world map.

---

## Technologies & Platforms Used
* **Cloud Infrastructure:** Microsoft Azure (Virtual Machines, Network Security Groups)
* **SIEM:** Microsoft Sentinel
* **Log Management:** Log Analytics Workspaces
* **Scripting:** PowerShell (Data extraction & API enrichment)
* **Query Language:** KQL (Kusto Query Language)
* **Data Visualization:** Azure Sentinel Workbooks
* **API:** IP-Geolocation.io

---

## Project Implementation

### 1. Data Collection & Enrichment
The core of the data collection was a custom PowerShell script that transformed raw Windows Security logs into actionable intelligence by adding geographic coordinates.

> **View the script here:** [Link to your script file in the repo]

### 2. Analytical Queries (KQL)
Once the data reached the cloud, I used **KQL** to parse the custom logs and prepare them for visualization:

kusto
FAILED_RDP_WITH_GEO_CL 
| extend location = strcat(latitude, ',', longitude)
| summarize event_count=count() by location, country, state, sourcehost

Log Lifecycle: Mastered the flow of data from local event generation to cloud-based analysis and visualization.

SIEM Proficiency: Developed skills in configuring Sentinel, managing Log Analytics Workspaces, and writing complex KQL queries.

### 3. Live Attack Visualization
The project culminated in the creation of a **Sentinel Workbook**. This interactive dashboard provided a real-time global map showing the density and origin of attacks. It allowed me to see exactly where in the world the brute-force attempts originated.

![World Attack Map]()
*Figure 1: Real-time map visualizing global RDP brute-force attempts.*

---

## Key Takeaways
* **Threat Landscapes:** Gained a firsthand look at how quickly exposed assets are discovered by automated botnets. Within minutes of deployment, attacks were logged from multiple countries.
* **Log Lifecycle:** Mastered the flow of data from local event generation to cloud-based analysis and visualization.
* **SIEM Proficiency:** Developed practical skills in configuring Sentinel, managing Log Analytics Workspaces, and writing complex KQL queries to handle custom logs.
