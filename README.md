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

# Cyber Threat Analytics Project: Day 3 Progress Report

## Executive Summary
Today, we completed Step 3: Temporal Analysis. Using our cleaned master telemetry file, we mapped out how traffic moves over time to differentiate routine automated background noise from aggressive, targeted cyber campaigns. 

Our deep dive focused on the two most targeted ports in the dataset: **Port 1433 (Microsoft SQL Server)** and **Port 5900 (VNC)**.

---

## 1. Lifespan Behavior & Volatility Analysis
By parsing our timestamps and resampling the raw data into daily chunks, we discovered that even though both ports have massive lifetime volumes, the threat actors behind them use completely opposite strategies.

### Port 5900 (VNC) — Constant Background Noise
* **Behavior:** Low volatility, non-stop automated scanning.
* **Top Metric:** Peaked at 396,678 attacks on November 18, 2025.
* **Daily Volatility (Standard Deviation):** 59,019.59
* **Analysis:** Port 5900 almost never drops to zero. Its low standard deviation mathematically proves that the traffic is highly stable and almost meets the daily average. This is the "digital background radiation" of the internet—botnets constantly crawling for exposed remote desktop access.

### Port 1433 (MSSQL) — High-Intensity Targeted Campaigns
* **Behavior:** Extreme volatility. Dead silent for months, followed by massive explosions of traffic.
* **Top Metric:** Peaked at 1,865,756 attacks on November 29, 2025.
* **Daily Volatility (Standard Deviation):** 247,659.61
* **Analysis:** The huge standard deviation proves that this port undergoes intense, coordinated campaigns. Attackers keep their infrastructure dormant, then spin up massive scanning clusters all at once to blitz database servers.

---

## 2. Advanced Threat Metrics & Anomaly Detection
To find true anomalies, we set a strict statistical threshold: any day where traffic exceeded **3 Standard Deviations** above the baseline mean (**55,852 daily attacks**) was flagged as a critical alert. 

Even with this high bar (threshold: **798,830 attacks**), **5 specific days** triggered alerts, exposing a distinct two-wave attack timeline:

* **Wave 1 (The Warning Shot):**
  * Nov 21, 2025: **1,275,089 attacks**
  * Nov 22, 2025: **823,636 attacks**
* **Wave 2 (The Blitz):**
  * Nov 28, 2025: **1,846,713 attacks**
  * Nov 29, 2025: **1,865,756 attacks** *(Project Peak)*
  * Nov 30, 2025: **1,305,659 attacks**

---

## 3. Hourly Forensic Investigation (November 29 Peak)
Zooming hour-by-hour into our project's peak day revealed the campaign's exact execution mechanics. This wasn't a quick script that ran for 5 minutes; it was a sustained, 24-hour marathon. 

The attackers maintained a crushing speed of **80,000 to 100,000 attacks every single hour**, hitting a specific maximum peak at **07:00 with 109,562 attacks**.

**Forensic Indicator:** Between 17:00 and 18:00, the attack volume plummeted from ~85k down to just **2,851 attacks**, before immediately ramping right back up to full capacity at 19:00. This highly specific 2-hour drop indicates either an attacker system crash/reboot, network mitigation by an upstream ISP, or target rate-limiting kicking in temporarily.

---

## Next Steps
Now that the temporal anomalies are cleanly mapped and quantified, we are ready for **Step 4: Cross-Feature Correlation / Geolocation Analysis**. We will cross-reference these late-November timestamp spikes against source IP addresses and country codes to map out the geographic footprint of the attacking botnet infrastructure.
