# MITRE ATT&CK Mapping

These mappings explain how comparable unauthorized actions can support adversary objectives. The observed actions were authorized lab administration; the event IDs alone do not establish an attack.

| Lab behavior | Relevant technique | Tactic | Evidence and qualification |
|---|---|---|---|
| Create a domain user | [T1136.002 — Create Account: Domain Account](https://attack.mitre.org/techniques/T1136/002/) | Persistence | Event 4720 shows `soc.test` created. Adversarial intent is not established. |
| Add the user to Domain Admins | [T1098.007 — Account Manipulation: Additional Local or Domain Groups](https://attack.mitre.org/techniques/T1098/007/) | Persistence; Privilege Escalation | Event 4728 shows privileged group membership added. This was an approved lab action. |
| Remove the privileged membership | Lab cleanup; no adversary technique assigned | Not applicable | Event 4729 documents removal, not evidence of malicious activity or complete session revocation. |

## Analyst conclusion

The exercise demonstrates evidence relevant to account creation and privilege-related group changes. It does not demonstrate that an attacker established persistence, used the privileges, or compromised the domain. Authorization context and follow-up investigation determine whether similar activity warrants an incident response.
