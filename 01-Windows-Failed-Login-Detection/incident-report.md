# SOC Incident Investigation Report

**Project:** Windows Failed Login Detection Using Splunk  
**Environment:** Windows 11 Virtual Machine  
**SIEM:** Splunk Enterprise  
**Log Source:** Windows Security Event Logs  
**Event ID:** 4625  
**Investigation Classification:** Lab Simulation — Suspicious Authentication Activity

## 1. Executive Summary

This investigation focused on identifying repeated Windows authentication failures using Splunk Enterprise.

Windows Security logs were collected from a Windows 11 virtual machine through Splunk Universal Forwarder and analyzed using Search Processing Language (SPL).

The final detection query identified a maximum of **12 failed authentication events within a fixed 30-minute interval on a single host**.

The investigation demonstrated the ability to identify authentication anomalies that may warrant further SOC analysis.

## 2. Detection Methodology

Windows Event ID 4625 was used to identify failed authentication attempts.

The detection logic grouped events by host and 30-minute time intervals, flagging intervals with three or more failed logons.

**Detection Threshold:** 3 or more failed authentication events per host within a fixed 30-minute interval.

## 3. Investigation Findings

- Windows Security logs were successfully ingested into Splunk.
- Repeated Event ID 4625 records were identified.
- The maximum observed failed authentication count was 12 within a 30-minute interval.
- Some events identified `WINDOW11$` as the subject computer account, while the failed target account was not identified.
- An inspected event showed loopback source address `127.0.0.1` and process `svchost.exe`.
- A separate controlled login test generated failed authentication activity associated with the lab account `dibsh`.
- An earlier scheduled detection rule successfully triggered an alert during testing.

## 4. MITRE ATT&CK Mapping

**Technique:** T1110 — Brute Force

Repeated authentication failures can be an indicator of brute-force attempts. However, the observed activity was not confirmed to be malicious, and the detection alone does not establish that a brute-force attack occurred.

## 5. Analyst Assessment

**Finding:** Repeated failed authentication events detected.

**Disposition:** Lab-generated or locally observed authentication failures; malicious activity not confirmed.

Further investigation would require reliable target-account extraction, additional source context, and correlation with successful logons.

## 6. Conclusion

This project demonstrated hands-on experience with Windows Security monitoring, Splunk log ingestion, SPL detection engineering, alert validation, and initial SOC investigation.

Future improvements include reducing false positives, improving account-level attribution, and correlating authentication failures with other security events.
