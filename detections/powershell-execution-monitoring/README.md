## Objective

The objective of this exercise was to simulate PowerShell command execution and analyze the resulting logs to determine whether the activity appeared benign or potentially malicious.

---

## Attack Simulation

A PowerShell command was encoded and executed on a Windows 10 endpoint to generate process creation logs for further analysis within Splunk.

![Command Encoding And Execution](screenshots/CommandEncodingAndExecution.png)

The following encoded command was used:

```powershell
powershell.exe -EncodedCommand RwBlAHQALQBQAHIAbwBjAGUAcwBzAA==
```

---

## SIEM Analysis

The initial query used to retrieve PowerShell-related process creation events was:

```spl
index=* "powershell" EventCode=4688
```

![Initial Query](screenshots/InitialPowerShellQuery.png)

The results contained numerous unrelated Splunk Universal Forwarder artifacts, which reduced visibility of relevant events. To refine the dataset, the following exclusion filter was applied:

```spl
NOT "SplunkUniversalForwarder\\bin\\splunk"
```

![Refined Query](screenshots/PowerShellQuerySplunkExclusion.png)

---

## Investigation Findings

The following fields were analyzed to determine the nature and context of the activity:

- Source IP address
- Target username
- Timestamp of events
- Creator Subject Account Name
- Process Command Line

These fields help distinguish between expected administrative activity and potentially suspicious execution patterns.

The primary PowerShell executions identified during the simulation included:

- `"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" Get-Date`
- `"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" Get-Service`
- `"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -EncodedCommand RwBlAHQALQBQAHIAbwBjAGUAcwBzAA=="`

---

## Decoding Analysis

The encoded PowerShell command was decoded to determine the underlying activity.

```powershell
[System.Text.Encoding]::Unicode.GetString(
    [System.Convert]::FromBase64String("RwBlAHQALQBQAHIAbwBjAGUAcwBzAA==")
)
```

The decoded output was:

```powershell
Get-Process
```

Although the decoded command was benign in this controlled lab environment, the use of encoded PowerShell commands may warrant additional investigation in a production SOC environment due to their association with obfuscation and defense evasion techniques.

---

## MITRE ATT&CK Mapping

- T1059.001 – Command and Scripting Interpreter: PowerShell  
- T1027 – Obfuscated Files or Information  

---

## Conclusion

The PowerShell activity observed during this exercise was generated intentionally within a controlled lab environment to simulate real-world detection and analysis scenarios.

No malicious activity or unauthorized execution was identified. The investigation demonstrated how PowerShell execution events can be identified, filtered, decoded, and analyzed within Splunk using Windows process creation logs.

The exercise also highlighted the importance of reviewing encoded commands and understanding execution context when assessing potential threats in a SOC environment.
