Situation: 

A detection indicated that a new local administrator account may have been created on an endpoint.

Investigation:

- Collected Windows Event Logs `Windows.EventLogs.EvtxHunter` from the endpoint using Velociraptor.
- Reviewed security events relating to account management activity.
- Identified evidence of a new account being created by searching for Event ID's 4720 (user account created) and 4732 (user account added to privilged group)
- Confirmed that the same account had subsequently been added to the local Administrators group.

Findings:

Account Created: tempadmin
Privileged Group: Administrators

Client command used
`net user tempadmin Password /add`
`net localgroup administrators tempadmin /add`

The sequence of events indicated that a newly created account had been granted elevated privileges. Determined that the account creation was iniated by the 'user' account. 

Outcome:

In a real environment, I would validate whether the activity was authorised, review related activity on the endpoint, and escalate if the behaviour could not be explained. Reaffirmed that the event ID 4732 is one of the most critical events for tracking privilege escalation and unauthorized access to administrative roles.