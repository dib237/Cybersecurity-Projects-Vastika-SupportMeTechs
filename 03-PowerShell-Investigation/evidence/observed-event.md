# Sanitized Evidence Transcript

**This is a curated transcription, not an original log export or a recreated screenshot.**

Source material: the operator's expanded event text and the supplied Splunk screenshot. The screenshot shows one marker match, the parent process, command line, and timestamp; other process details below come from the pasted event.

| Field | Sanitized or retained value |
|---|---|
| Displayed event time | 2026-10-29 23:59:24.270; time zone not independently verified |
| Log / event / record | Security / 4688 / 68075 |
| Host | LAB-HOST (replacement) |
| Creator account | LAB-USER (replacement) |
| Creator domain | LAB-HOST (replacement) |
| Creator SID / Logon ID | Omitted |
| New process ID | 0x27cc |
| New process name | C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe |
| Parent process ID | 0x267c |
| Parent process name | C:\Windows\System32\cmd.exe |
| Token type | TokenElevationTypeFull (2) |
| Mandatory label | S-1-16-12288 |
| Command line | powershell.exe -noprofile -command "write-output 'soc-p3-controlled-test'" |

Command-line spacing is normalized for readability. Paths are standard executable locations, not user profile paths. Browser URL, browser account UI, original host, personal account name, account SID, and logon identifier are not published.

The screenshot's search window displays 2026-10-29 23:45:59 through 2026-10-30 00:00:59, with one matching event. This is the count for that search, not all PowerShell activity.

The unredacted screenshot remains outside the public repository. No image was generated or edited to stand in for original evidence.
