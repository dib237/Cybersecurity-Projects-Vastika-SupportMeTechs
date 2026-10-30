# Splunk Alert Configuration and Validation

## Overview

This document describes the scheduled alert configured and tested during the Windows Failed Login Detection lab.

## Alert Details

**Alert Name:** SOC - Brute Force Login Detection  
**SIEM Platform:** Splunk Enterprise  
**Log Source:** Windows Security Event Logs  
**Event ID:** 4625

## Original Alert Configuration

- **Detection threshold:** 5 or more failed authentication events within a 5-minute bucket
- **Grouping:** Extracted `Account_Name` field
- **Schedule:** Every 5 minutes
- **Cron expression:** `*/5 * * * *`
- **Search time range:** Earliest `-5m@m`, latest `now`
- **Trigger condition:** Number of results greater than 0
- **Trigger frequency:** Once
- **Alert action:** Add to Triggered Alerts

## Alert Validation

The original scheduled alert successfully triggered during lab testing.

One observed alert result showed six events associated with the extracted account field `WINDOW11$`.

Subsequent raw-event investigation showed that `WINDOW11$` represented the subject computer account in the inspected event, rather than a confirmed failed target account.

Therefore, the alert demonstrated successful scheduled detection and triggering, but did not establish an attack against a specific user.

## Final Detection Rule

The project later adopted a simpler host-based detection:

```spl
index=main
source="WinEventLog:Security"
EventCode=4625
| bin _time span=30m
| stats count as FailedAttempts by _time host
| where FailedAttempts>=3
| sort - _time
```

The final rule successfully returned matching results, including a maximum observed count of 12 failed authentication events in one 30-minute interval.

**Important:** The final query was validated through Splunk search. The previously triggered scheduled alert used the original configuration; the final rule has not been verified as deployed in that alert.

## Lessons Learned

- Successful alert triggering does not automatically establish malicious activity.
- Extracted fields must be checked against raw Windows events.
- Threshold-based authentication detections require tuning and investigation.
- Detection validation and alert deployment should be documented separately.
