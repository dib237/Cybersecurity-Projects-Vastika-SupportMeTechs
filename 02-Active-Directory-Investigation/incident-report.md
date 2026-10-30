# Active Directory Investigation Report

**Classification:** Authorized lab exercise  
**Disposition:** Expected administrative changes; no malicious activity established  
**Evidence date:** October 29, 2026  
**Host:** `DC1.diwash.local`

## Executive summary

The lab account `DIWASH\soc.test` was created, added to Domain Admins, and removed from that group. Three Event Viewer screenshots record the sequence. Investigation consisted of manually filtering Windows Security events and comparing the account, group, host, and displayed timestamps.

## Evidence and timeline

| Evidence | Event | Displayed local time | Supported observation |
|---|---|---|---|
| [01](screenshots/2-01-user-creation.png) | 4720 | 10/29/2026 10:24:45 PM | New account `soc.test`, domain `DIWASH`, display name `SOC Test` |
| [02](screenshots/2-02-privileged-group-added.png) | 4728 | 10/29/2026 10:47:03 PM | Member `DIWASH\soc.test` added to `DIWASH\Domain Admins` |
| [03](screenshots/2-03-privileged-group-removed.png) | 4729 | 10/29/2026 10:50:02 PM | Same member removed from the same group by `DIWASH\Administrator` |

All three show the Security log, Audit Success, and `DC1.diwash.local`. The VM time zone is not visible. The creation-to-addition interval is 22 minutes 18 seconds; the addition-to-removal interval is 2 minutes 59 seconds.

## Attribution

- **Actor (Subject):** `DIWASH\Administrator` for all three actions, confirmed by the lab operator. Only screenshot 03 directly displays this Subject.
- **Affected user (Member/New Account):** `DIWASH\soc.test`.
- **Member distinguished name:** `CN=SOC Test,CN=Users,DC=diwash,DC=local`, visible in the addition and removal records.
- **Affected group:** `DIWASH\Domain Admins`.
- **Removal Subject Logon ID:** `0x784C8`, visible in screenshot 03. This is not evidence that the earlier actions used the same logon session.

The Event Viewer footer's `User: N/A` is not the actor field. The Subject section identifies the principal performing the operation.

## Analysis and response

A new domain account gaining privileged membership warrants review outside an approved lab or change window. Here, the sequence matches the operator's authorized exercise. Event 4729 supports removal of the membership as cleanup; it does not establish immediate invalidation of existing sessions or prove the account has no other privileges.

No evidence of credential theft, unauthorized persistence, lateral movement, or use of the granted privileges was provided. The account was retained; no deletion event was collected.

## Evidence limits and follow-up

The evidence consists of screenshots, not exported EVTX/XML records. Numeric SIDs, event record IDs, full Subject details for the first two events, and time-zone settings are not available. Account correlation therefore uses the displayed names, distinguished name, host, and chronology rather than a verified numeric SID join.

For a fuller case record, export the original events, capture the first two Subject sections, verify current group membership, and examine relevant logons. These are future improvements, not completed work claimed by this report.
