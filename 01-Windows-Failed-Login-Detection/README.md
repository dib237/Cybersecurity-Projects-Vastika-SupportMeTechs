
# Windows Failed Login Detection Using Splunk

## SOC Portfolio Project 1

### Project Overview
This project demonstrates how to detect and investigate repeated Windows authentication failures using Splunk Enterprise and Windows Security Event ID 4625.

### Lab Environment
- Windows 11 Virtual Machine
- Splunk Enterprise
- Splunk Universal Forwarder
- Windows Security Event Logs

### Detection Results
- Event ID: 4625
- Detection threshold: 3 or more failed logons per host in a fixed 30-minute interval
- Maximum observed: 12 failed authentication events
- Scheduled alert successfully triggered during earlier testing

### MITRE ATT&CK
T1110 - Brute Force (potential indicator, not a confirmed attack)

### Project Documentation
- SPL detection query
- SOC incident investigation report
- MITRE ATT&CK mapping
- Detection screenshots
