**Objectives**

Simulate repeated failed login attempts and validate SIEM detection capabilities.
Will be analysed using splunk after generating alerts. 

**Attack Simulation**

A Windows endpoint was accessed on Windows 10, and multiple incorrect password attempts were performed to generate failed authentication events. (EventCode 4625)
![Windows VM Failed Login](screenshots/WindowsVMFailedLogin.png)


Once the logs were generated they were forwarded to Splunk for analysis. The first step was to index the logs around the time the logs were generated, for this exercise the 24 hour was enough. In a real environment this would be too broad of a time frame and would need to be narrowed for a focused view of the incident. The query Index=* was used to retrieve logs as well as EventCode=4625 for more specificity
![FailedLogonQueries](screenshots/FailedLogonQueries.png)

When analyzing the logs specific information such as the source IP address, the account name, time, failure reason to compare to other log entries for contextualization and compared to other logs. Due to the nature of the simulation the other logs would show the same information however if it were a case where there were various failed logon attempts from a variety of different endpoints this is usually an indicator of a password spraying attack or if it were the same endpoint with failed logins in rapid succession there would be a possibility of a brute force attack.
These would all fall under the MITRE attack framework technique ID T1110, with the sub technique IDs being T1110.003 for password spraying and  T1110.001 for password guessing. 

**Conclusion**

The endpoint was logged into with the correct password after a number of tries which can be interpreted as a simple user error before being successful and no further remediation would be required.
