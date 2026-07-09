# Cyber-Threat-Analytics
Summers Project 

## Project Status: Environment Setup Complete
- Created Python workspace in Google Colab.
- Initialized public repository framework.
- Sourced and structured 4 foundational honeypot threat datasets from Kaggle.
- Set up complete for project to be started, checked the links of the datasets from drive to the Google Colab code.

# Technical Progress Report: Day 2
**Project:** Cyber Threat Anomaly & Strategic Analytics Engine
**Focus Area:** Explored Attack Surface Area & Baseline Aggregation

## 1. Objective
To systematically isolate, aggregate, and rank the total attack volumes across all network endpoints within the unified telemetry dataset. This establishes our statistical baseline—representing the "normal" background cyber noise—so we can accurately identify anomalies and spikes in future phases.

## 2. Engineering & Data Extraction Methodology
A dynamic data engineering script was developed using Python and the `pandas` library to programmatically parse our master telemetry schema. 
- **Column Filtering:** Isolated specific target columns by matching the `Attack_counts_` prefix combined with trailing numerical port identifiers.
- **Aggregation Strategy:** Computed the column-wise sum across millions of records to determine absolute attack frequencies per protocol, sorting the final metrics in descending order to isolate the highest-velocity threat vectors.

## 3. Empirical Findings (Top Targeted Vectors)
The aggregation script exposed an intense focus on legacy remote access protocols, database infrastructure, and internal network sharing services:

- **Port 1433 (Microsoft SQL Server):** 9,941,662 total attacks logged
  *Implication:* The most heavily targeted port in the dataset, indicating relentless automated brute-forcing attempts seeking database access and structured data exfiltration.
- **Port 5900 (VNC Remote Desktop):** 9,208,102 total attacks logged
  *Implication:* Massive volume directed at unauthorized graphical remote control tools, typical of attackers looking for easy-to-exploit interactive sessions.
- **Port 445 (Server Message Block / SMB):** 8,010,145 total attacks logged
  *Implication:* Highly targeted due to historical vulnerabilities (e.g., EternalBlue). This reflects automated scanning designed for lateral movement and network worm propagation.
- **Port 22 (Secure Shell / SSH):** 7,737,273 total attacks logged
  *Implication:* Continuous background noise of automated credential-stuffing and password-spraying attacks targeting secure terminal access.
- **Port 23 (Telnet):** 440,571 total attacks logged
  *Implication:* Lower volume but consistent traffic targeting unencrypted legacy systems and vulnerable Internet of Things (IoT) devices.

## 4. Analytical Summary & Next Steps
The data proves that network perimeter threats are not evenly distributed; the vast majority of malicious traffic is highly concentrated on just four critical access ports (1433, 5900, 445, and 22). 
With this target baseline firmly established, the next phase will transition from static volumetric totals into **Temporal Analysis & Statistical Anomaly Detection**. We will map these specific high-volume ports against our standardized timeline to calculate rolling Z-scores and flag real-time attack spikes.
