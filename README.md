# HomeLab-and-SIEM-

**Overview**

This repository contains a variety of cybersecurity incident scenarios analyzed and documented within a home SOC lab environment. The focus is on log analysis, alert triage, investigation workflow, and documenting appropriate remediation or escalation steps commonly performed in a professional SOC environment.

**Architecture** 

The lab architecture consists of three virtual machines: Kali Linux used to simulate attacker activity, Windows 10 serving as the target endpoint, and an Ubuntu Server instance hosting Splunk Enterprise for log ingestion, monitoring, and incident analysis. 

**Data Flow** 

Event logs are generated on the target endpoint through direct system interaction (e.g., failed login attempts) or simulated attacker activity from Kali Linux. These logs are forwarded to Splunk Enterprise using Splunk Universal Forwarder to enable centralized monitoring, analysis, and investigation of security events.
