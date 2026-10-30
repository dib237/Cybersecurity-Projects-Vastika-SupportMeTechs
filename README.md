# Cybersecurity-Projects-Vastika/SupportMeTechs


Welcome to my hands-on cybersecurity portfolio, featuring practical security monitoring, detection engineering, incident investigation, and Windows security projects.

These projects demonstrate my experience working with SIEM platforms, endpoint security logs, identity systems, and SOC investigation workflows.

## Technical Skills

- **SIEM & Detection:** Splunk Enterprise, SPL, security alerting
- **Windows Security:** Event Viewer, Windows Security Logs, PowerShell
- **Identity & Access:** Active Directory, Group Policy, account management
- **Security Analysis:** Authentication monitoring, log correlation, incident investigation
- **Frameworks:** MITRE ATT&CK

## SOC Projects

### Project 01 — Windows Failed Login Detection Using Splunk

**Status: Completed**

Developed and tested an SPL detection rule to identify repeated Windows authentication failures using Security Event ID 4625.

**Highlights:**
- Configured Windows Security log forwarding to Splunk Enterprise.
- Detected 12 failed authentication events in the selected lab bucket on one host within a fixed 30-minute interval.
- Successfully tested scheduled alerting with an earlier detection rule.
- Investigated authentication event details and documented findings.
- Mapped the detection use case to MITRE ATT&CK T1110.

[View Project 01](01-Windows-Failed-Login-Detection/README.md)

### Project 02 — Active Directory Investigation

**Status: Completed — manual lab investigation**

Created a test AD user, temporarily added it to Domain Admins, and investigated Windows Security events using Event Viewer.

**Highlights:**
- Documented user creation (4720), privileged group addition (4728), and removal (4729).
- Built an evidence-based timeline with three original screenshots.
- Distinguished operator-confirmed actor details from directly visible evidence.
- Mapped the lab behavior to MITRE ATT&CK T1136.002 and T1098.007 without claiming malicious activity.

[View Project 02](02-Active-Directory-Investigation/README.md)

### Project 03 — PowerShell Process Investigation Using Splunk

**Status: Completed — controlled execution and manual investigation**

Captured a benign PowerShell marker command in Windows Security event 4688 and investigated it in Splunk.

**Highlights:**
- Enabled process creation auditing and command-line collection in the lab.
- Verified the cmd.exe to powershell.exe process chain and marker command.
- Distinguished the test process from Splunk's PowerShell helper.
- Published a sanitized evidence transcript, report, validation search, and MITRE T1059.001 mapping.
- Documented that a marker lookup does not establish malicious activity or validate a general behavioral detector.

[View Project 03](03-PowerShell-Investigation/README.md)

## Portfolio Objective

My goal is to develop practical SOC analyst skills through hands-on security labs, realistic detection scenarios, investigation reports, and technical documentation.

Each project focuses on building detection logic, analyzing evidence, understanding limitations, and communicating findings clearly.
