# Collection and Validation Workflow

## Lab prerequisites

Windows 11, Windows PowerShell 5 (operator-reported major version), Splunk Universal Forwarder, and Security logs arriving in Splunk's `main` index. Scope any audit-policy changes to your authorized lab.

## Logging changes used

In Administrator Command Prompt:

```cmd
auditpol /get /subcategory:"Process Creation"
auditpol /set /subcategory:"Process Creation" /success:enable
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Audit" /v ProcessCreationIncludeCmdLine_Enabled /t REG_DWORD /d 1 /f
```

Process creation auditing and command-line inclusion are separate settings. Changes affect new events; they do not populate historical blank command lines. Command arguments are recorded in plain text, so do not place secrets in lab commands.

## Generate and find the marker

Run in Command Prompt:

```cmd
powershell.exe -noprofile -command "write-output 'soc-p3-controlled-test'"
```

After forwarding, use [detection.spl](detection.spl) in Splunk with an appropriate time window. The demonstrated search also specified the original lab host. That identifying host filter is omitted in the public query; add your own host filter in a multi-endpoint environment.

The public query uses the same marker, event code, index, and observed Security source. Its exact source-scoped variant was not rerun in the lab; the screenshot validates the host-scoped marker search. This is a marker lookup, not a behavioral alert.

## Investigate before classifying

Expand the event and verify New Process Name, Creator Process Name, Creator Subject, timestamp, token context, and Process Command Line. A broad raw-text search for PowerShell can match parent processes or `splunk-powershell.exe`; inspect the child executable explicitly.

## Future work

A future suspicious-behavior rule should define the behavior it seeks, validate benign and negative cases, and document false positives. Script-block logs or Sysmon could enrich that work, but neither is required for the demonstrated 4688 pipeline.

## References

- [Microsoft: command-line audit policy](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-admx-auditsettings)
- [Microsoft: Event 4688](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4688)
