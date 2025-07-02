
# 🔍 SIEM Log Monitoring & Alerting with Splunk

## 📌 Project Overview
This project simulates the real-world role of a Tier 1 SOC Analyst using Splunk to monitor security logs, detect common attacks, and trigger alerts.

## 🛠 Tools & Technologies
- Splunk Enterprise (Free)
- Windows Security Logs & Sysmon
- MITRE ATT&CK Framework
- TryHackMe Labs (SOC Level 1, Splunk 101)

## 🧱 Setup Instructions
1. Install Splunk: https://www.splunk.com/en_us/download/splunk-enterprise.html
2. Add an index: `security_logs`
3. Forward logs or manually upload:
   - Windows Event Logs (EventCode 4625, 4624, 4672)
   - Sysmon logs (process creations, network connections)

## 🚨 Detection Rules

### Brute Force Detection
```
index=security_logs sourcetype=WinEventLog:Security EventCode=4625
| stats count by src_ip, user, _time
| where count > 5
```

### Privilege Escalation
```
index=security_logs EventCode=4672
| stats count by user, host
```

### RDP Login Attempt
```
index=security_logs EventCode=4624 Logon_Type=10
| stats count by user, src_ip
```

## 🎯 MITRE ATT&CK Mapping

| Threat               | Tactic               | Technique       | ID     |
|----------------------|----------------------|------------------|--------|
| Brute Force          | Credential Access    | Brute Force      | T1110  |
| Privilege Escalation | Privilege Escalation | Admin Accounts   | T1078  |
| RDP Logins           | Lateral Movement     | Remote Services  | T1021  |

## 📸 Screenshots
> Add screenshots of:
- Detection dashboards
- Alert rules
- Triggered alerts

## 📁 Folder Structure
```
splunk-log-monitoring/
├── detections/
│   └── alert_queries.spl
├── screenshots/
├── reports/
│   └── incident_summary.md
└── README.md
```

## 🧠 Learning Outcomes
- Built a working detection pipeline in Splunk
- Mapped techniques to MITRE ATT&CK
- Demonstrated alerting and reporting for SOC workflows

## 🧑‍💼 About Me
I'm preparing for the CompTIA Security+ SY0-701 and working towards a career as a SOC Analyst. This project reflects my ability to detect and respond to real security events.
