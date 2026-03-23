#  SSH Log Analysis & Brute Force Detection Using Splunk

##  Project Overview
This project focuses on analyzing SSH authentication logs using Splunk to detect suspicious activities such as brute-force attacks, failed login attempts, unauthorized access, and successful logins.

It simulates real-world SOC analyst workflows including log ingestion, analysis, dashboard creation, and alert configuration.

---

##  Objectives
- Detect successful SSH logins
- Identify failed login attempts
- Detect brute-force attacks (multiple failed attempts)
- Identify connections without authentication
- Perform log analysis using SPL

---

##  Tools & Technologies
- Splunk Enterprise
- SPL (Search Processing Language)
- Zeek SSH Logs (JSON)

---

##  Dataset Information
The dataset includes:
- Source IP (id.orig_h)
- Destination Host (id.resp_h)
- Event Type (login, failed, brute-force)
- Authentication Status
- Number of Attempts

Example log:{ "id.orig_h": "10.0.0.36", "event_type": "Failed SSH Login", "auth_attempts": 1 }


---

##  Implementation Steps

### 1. Data Ingestion
- Uploaded SSH logs into Splunk
- Source type: _json
- Index: ssh_logs

 As shown in your setup steps (page 5) :contentReference[oaicite:0]{index=0}

---

##  SPL Queries

###  Validate Data
index=ssh_logs| stats count by event_type


###  Failed Login Attempts
index=ssh_logs event_type="Failed SSH Login"| stats count by id.orig_h| sort -count| head 10


###  Brute Force Detection
index=ssh_logs event_type="Multiple Failed Authentication Attempts"| stats count by id.orig_h, id.resp_h| where count > 5


###  Successful Logins
index=ssh_logs event_type="Successful SSH Login"| stats count by id.orig_h



---

##  Dashboard
Created a Splunk dashboard to visualize:

- Failed login attempts by IP
- Brute-force attack patterns
- Successful login distribution
- Unauthorized connection attempts

 Example visualization includes bar charts of failed logins (page 12) :contentReference[oaicite:1]{index=1}

---

##  Alert Configuration
Configured alerts for:

- More than 5 failed attempts within 10 minutes
- Suspicious login patterns

 Alert setup based on brute-force detection (page 14) :contentReference[oaicite:2]{index=2}

---

##  Security Insights
- Detection of brute-force attacks
- Identification of suspicious source IPs
- Detection of unauthorized connection attempts
- Monitoring authentication behavior

---

##  Project Files
- SSH Log Analysis Report (PDF)
- SSH Logs Dataset (JSON)

---

##  Future Enhancements
- Add geo-location analysis of IPs
- Integrate threat intelligence feeds
- Enhance dashboard visualization

---

##  Author
Shreedhar Teradal  
Aspiring Cybersecurity Analyst
