Situation: 

- An alert indicates suspicious PowerShell activity on an endpoint.

Investigation:

- Collected Windows Event Logs `Windows.EventLogs.EvtxHunter` from the endpoint using Velociraptor.
- Reviewed PowerShell executable events for evidence of unusual execution.
- Identified a PowerShell session launched using command-line arguments commonly associated with attacker tradecraft.
- Examined the execution context to determine what command had actually run.

Findings:

PowerShell was executed with the following command:

`powershell.exe -nop -w hidden Get-Process`

The use of:

`-nop `(NoProfile), and `-w hidden` (Hidden Window) is commonly seen in post-exploitation activity designed to reduce visibility. In this case, the underlying command (Get-Process) was benign, it lists the processes running.

Outcome

- Determined that the activity did not represent malicious execution in this instance.
- Demonstrated the importance of distinguishing suspicious characteristics from malicious intent.
- Recommend further investigation of the user context and any related or susbsequent activity.