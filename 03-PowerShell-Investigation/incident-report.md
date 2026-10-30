# PowerShell Incident Investigation Report

**Classification:** Authorized lab validation  
**Disposition:** Benign controlled execution; no malicious activity established  
**Evidence:** One Splunk screenshot plus a pasted expanded event; sanitized for publication

## Finding

At the displayed time October 29, 2026, 11:59:24.270 PM, Windows recorded a PowerShell process launched by Command Prompt. The command line contains the unique lab marker. The final screenshot shows one matching event for its selected 15-minute window.

The creator account is represented here as `LAB-USER` on `LAB-HOST`. The expanded event showed an elevated token (type 2) and high integrity label S-1-16-12288. These describe execution context; elevation alone is not evidence of compromise.

## Process analysis

- Child: `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`, PID `0x27cc`.
- Parent: `C:\Windows\System32\cmd.exe`, PID `0x267c`.
- Command: `powershell.exe -noprofile -command "write-output 'soc-p3-controlled-test'"`.
- Expected behavior: print a lab marker and finish.
- Verified behavior: event 4688 records process creation with that command line; Splunk received it.

The record does not establish that the command completed successfully or that no other activity occurred on the host. The ordinary Windows executable path does not independently verify binary signature or integrity.

## Investigation sequence

1. Confirmed that Splunk was receiving Windows Security logs.
2. Found historical 4688 events but no matching new PowerShell test.
3. The operator reported Process Creation auditing as No Auditing, then successfully enabled success auditing.
4. A broad PowerShell text search returned six matching events; one inspected result was `splunk-powershell.exe` launched by `splunkd.exe` under the forwarder service account. This was not the controlled test.
5. Narrowing to the new executable ending in `\powershell.exe` returned two results. An inspected PowerShell event at 11:51:39.347 PM had a blank command line.
6. The operator enabled command-line inclusion and reran the benign command.
7. The final event at 11:59:24.270 PM included the marker and the command line.

The six, two, and one results came from different queries/windows. They are not a common denominator or a measured detection rate. Initial logging settings and intermediate searches are operator-provided observations rather than separately captured screenshots.

## Assessment

The evidence matches the authorized lab command. Neither `-NoProfile`, an elevated token, nor PowerShell execution alone establishes malicious intent. No encoded payload, download, persistence, or credential theft was demonstrated.

No containment was required for the marker command. No claim is made that logging settings were reverted. Additional validation could include binary verification, process termination evidence, and a documented benign/negative test set for a future behavioral rule.

## Evidence limitations

The screenshot uses a collapsed event view: it visibly shows the marker, parent process, timestamp, search, and result count. Child path, creator identity, elevation, and other details come from the separately pasted expanded event. No raw EVTX export, Sysmon record, or event 4104 from this run was provided.
