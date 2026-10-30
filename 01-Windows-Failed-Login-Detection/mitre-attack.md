# MITRE ATT&CK Mapping — Windows Failed Login Detection

## Technique Information

**MITRE ATT&CK Technique:** T1110 — Brute Force  
**Tactic:** Credential Access  
**Reference:** https://attack.mitre.org/techniques/T1110/

## 1. Technique Overview

Brute-force attacks involve repeated authentication attempts to obtain unauthorized access to accounts or systems.

Windows Security Event ID 4625 records failed logon attempts and can provide useful evidence when investigating possible brute-force activity.

## 2. Detection Logic

The Splunk detection monitors Windows Security Event ID 4625 and identifies hosts with three or more failed authentication events within fixed 30-minute intervals.

During testing, the highest observed count was 12 failed authentication events within one interval.

## 3. Why This Maps to T1110

Repeated authentication failures may indicate password guessing or other brute-force behavior.

However, authentication failures can also occur because of incorrect credentials, background services, or configuration problems.

The observed lab activity was not confirmed as malicious. This project maps the detection use case to T1110, rather than claiming that an actual brute-force attack occurred.

## 4. Detection Limitations

- The detection counts failures per host rather than per target account or source IP.
- Some observed events did not identify the failed target account.
- Fixed 30-minute time buckets may split activity across intervals.
- The rule does not distinguish malicious attempts from ordinary authentication errors.
- Additional log correlation is needed to determine whether an attack occurred.

## 5. Recommended Improvements

- Extract and validate target usernames.
- Correlate failed logons by source IP and target account.
- Investigate successful logons following repeated failures.
- Tune thresholds to reduce false positives.
- Enrich alerts with account and endpoint context.

## 6. SOC Analyst Takeaway

This project demonstrates how to map an authentication anomaly detection to a relevant MITRE ATT&CK technique while documenting the limitations of the available evidence.
