## Objective

The objective of this exercise was to simulate repeated failed login attempts and validate detection and analysis capabilities using Splunk SIEM.

---

## Attack Simulation

A Windows 10 endpoint was used to generate failed authentication events by repeatedly entering incorrect credentials for a local user account. This activity generated Windows Event ID 4625 (failed logon attempts).

![Windows VM Failed Login](screenshots/WindowsVMFailedLogin.png)

---

## Log Ingestion and SIEM Analysis

Once generated, logs were forwarded to Splunk for analysis. The investigation focused on authentication events within a 24-hour time window to identify failed login patterns.

In a production environment, this time range would typically be narrowed to improve investigation efficiency based on alert timestamps.

The following query was used to retrieve relevant events:

```
index=* EventCode=4625
```

![Failed Logon Queries](screenshots/FailedLogonQueries.png)

---

## Investigation Findings

Key fields were analyzed to determine the nature and scope of the activity:

- Source IP address
- Target username
- Timestamp of events
- Failure reason codes
- Frequency of login attempts

This analysis helps distinguish between isolated user error and potential attack patterns.

In this simulation, all failed login attempts originated from a single endpoint within the controlled lab environment.

If multiple endpoints or distributed sources were observed, this could indicate password spraying activity. A high volume of rapid attempts against a single account could indicate brute force behavior.

---

## MITRE ATT&CK Mapping

- T1110 – Brute Force  
  - T1110.001 – Password Guessing  
  - T1110.003 – Password Spraying  

---

## Conclusion

The successful authentication observed during testing was part of the controlled simulation and not indicative of malicious activity.

No evidence of unauthorized access or lateral movement was identified, and no remediation actions were required beyond validation of detection capability.
