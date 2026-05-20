## HomeLab-and-SIEM

---

## Overview

This repository contains cybersecurity incident scenarios analyzed within a home SOC lab environment. The focus is on log analysis, alert triage, investigation workflows, and documentation of findings in a SOC-style format.

---

## Architecture

The lab consists of three virtual machines:

- Kali Linux (attack simulation)
- Windows 10 (target endpoint)
- Ubuntu Server (Splunk Enterprise)

Splunk is used for centralized log ingestion, monitoring, and security event analysis.

---

## Data Flow

Event logs are generated on the Windows endpoint through system activity and simulated attack behavior from the Kali Linux VM.

These logs are forwarded to Splunk Enterprise via Splunk Universal Forwarder for centralized analysis and detection.

Once ingested, logs are analyzed within Splunk to identify suspicious behavior, investigate alerts, and correlate events across the environment.
