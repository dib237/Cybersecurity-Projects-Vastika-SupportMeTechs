# Detection and Event Review

## Method used

On the domain controller, open **Event Viewer → Windows Logs → Security → Filter Current Log**. Filter individually for `4720`, `4728`, and `4729`, refreshing the view after each operation. Inspect the event contents rather than relying on the event ID alone.

| ID | Meaning | Fields to review |
|---|---|---|
| 4720 | User account created | New Account, domain, Subject, computer, time |
| 4728 | Member added to security-enabled global group | Member, Group, Subject, computer, time |
| 4729 | Member removed from security-enabled global group | Member, Group, Subject, computer, time |

For this case, match `soc.test` and `DIWASH`; for membership changes, also match `Domain Admins`. A single relevant addition is enough to investigate; this project does not use an event-count threshold.

## Interpretation

The Subject is the actor; the Member is the account or group whose membership changed; the Group is the destination. A 4728 event can concern any security-enabled global group, so the group must be checked before labeling the change privileged.

Correlation by numeric SID is preferable when full records are available: the created account's TargetSid can be compared with the membership event's MemberSid. In membership events, TargetSid describes the group. Numeric SIDs were not visible in this evidence set, so that correlation was not performed.

## Scope and limitations

This is a manual Event Viewer investigation, not continuous monitoring or an automated alert. The demonstrated sequence covers a global group. Local and universal group membership changes use other event IDs and are outside the tested scope.

If events are absent, check the correct domain controller, filters, refresh state, and effective success auditing for User Account Management and Security Group Management. Enabling auditing after an operation does not recreate its historical event.

## References

- [Microsoft: Event 4720](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4720)
- [Microsoft: Audit Security Group Management](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/audit-security-group-management)
