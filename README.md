# HomeLab-and-SIEM-

**Overview**- This repository contains a variety of cybersecurity incident scenarios analyzed and documented within a home SOC lab environment. The focus is on log analysis, alert triage, investigation workflow, and documenting appropriate remediation or escalation steps commonly performed in a professional SOC environment.

**Architecture** - The lab architecture consists of three virtual machines: Kali Linux used to simulate attacker activity, Windows 10 serving as the target endpoint, and an Ubuntu Server instance hosting Splunk Enterprise for log ingestion, monitoring, and incident analysis. Windows event logs are forwarded to Splunk using Splunk Universal Forwarder to enable centralized monitoring and investigation of security events.
