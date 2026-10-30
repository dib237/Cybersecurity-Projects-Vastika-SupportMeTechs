# Lab Workflow

This records an authorized AD lab exercise. Perform privileged membership changes only in an isolated lab under your control.

## Completed sequence

1. In Active Directory Users and Computers, create the user `soc.test` with display name `SOC Test` in the lab domain's Users container.
2. Find Security event 4720 in Event Viewer and capture the account details.
3. Temporarily add the test user to Domain Admins through **Properties → Member Of**.
4. Find event 4728 and verify the Member and Group fields; capture the evidence.
5. Remove the test user from Domain Admins while retaining the account.
6. Find event 4729 and capture the Subject, Member, and Group fields.
7. Compare the three events and document the timeline and evidence limits.

## Collection status

Three screenshots were collected from the domain controller's Security log. No raw EVTX export, automated collection pipeline, alert configuration, or PowerShell execution is asserted. The visible Audit Success records establish that these operations were logged; the effective audit-policy configuration itself was not captured.

## Additional validation for a repeat run

Before starting, verify success auditing for user-account and security-group management. After cleanup, independently check the user's current membership and preserve complete event records with timestamps and numeric SIDs. These checks would strengthen the evidence but are not represented as performed in the supplied screenshots.
