# MITRE ATT&CK Mapping

**Technique:** [T1059.001 — Command and Scripting Interpreter: PowerShell](https://attack.mitre.org/techniques/T1059/001/)  
**Tactic:** Execution

PowerShell can be abused to execute adversary commands. This lab exercises telemetry relevant to that technique through a harmless marker command.

Event 4688 records the PowerShell invocation, parent Command Prompt, and command line. This supports an execution investigation; it does not establish adversarial use of the technique.

No other tactics or techniques are asserted. In particular, no evasion, persistence, credential access, or lateral movement was demonstrated.
