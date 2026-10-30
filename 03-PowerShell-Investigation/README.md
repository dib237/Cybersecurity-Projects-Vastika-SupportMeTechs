# PowerShell Process Investigation Using Splunk

**SOC Portfolio Project 03 | Windows Event 4688 | Process Investigation**

**Status: Completed — controlled execution and manual investigation.** This is the benign validation phase of the Suspicious PowerShell project, not a validated malicious-behavior detector.

## Overview

Generated harmless PowerShell activity in a Windows 11 lab, collected Windows Security process-creation events through Splunk Universal Forwarder, and located the command in Splunk. Investigated the parent process, executable, account context, elevation, and command line.

**Flow:** Windows 11 → Security event 4688 → Universal Forwarder → Splunk → manual investigation.

Sysmon was not used. Recent PowerShell Operational events were unavailable during troubleshooting, so the demonstrated route uses Security logs rather than event 4104.

## Controlled activity

Run inside the lab's Command Prompt:

```cmd
powershell.exe -noprofile -command "write-output 'soc-p3-controlled-test'"
```

The command prints a marker. It performs no download, persistence, or credential access. Process creation and command-line capture confirm the invocation; the audit record does not capture console output or an exit code.

## Observed result

| Field | Evidence |
|---|---|
| Event | Security 4688, Audit Success |
| Displayed time | October 29, 2026, 11:59:24.270 PM |
| Process chain | cmd.exe → powershell.exe |
| New process | C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe |
| Parent process | C:\Windows\System32\cmd.exe |
| New / parent PID | 0x27cc / 0x267c |
| Elevation | TokenElevationTypeFull (2) |
| Command | powershell.exe -noprofile -command "write-output 'soc-p3-controlled-test'" |
| Final marker search | One event in the screenshot's 15-minute window |

The screenshot's search window runs from October 29 at 11:45:59 PM through October 30 at 12:00:59 AM. Display times are retained without assuming a time zone.

## Documentation

- [Incident investigation report](incident-report.md)
- [Validated marker search](detection.spl)
- [Collection and validation workflow](lab-workflow.md)
- [MITRE ATT&CK mapping](mitre-attack.md)
- [Sanitized evidence transcript](evidence/observed-event.md)

## Evidence and privacy

Reviewed one supplied Splunk screenshot and the operator's pasted expanded event. The public evidence is a labeled transcription, not an original EVTX export. Personal account, machine identifiers, full account SID, logon ID, and browser details are omitted or replaced. The unredacted screenshot is not uploaded.

## Outcome and limits

The lab verified process auditing, command-line collection, forwarding, search, and manual attribution. The test was authorized and benign. A marker search is a validation aid, not general suspicious-PowerShell detection. No scheduled alert, malicious payload, script-block capture, process exit status, or full endpoint investigation is claimed.
