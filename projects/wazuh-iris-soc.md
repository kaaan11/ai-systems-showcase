# Wazuh–IRIS SOC

**A defensive SOC automation and investigation project built around Wazuh and DFIR-IRIS.**

> **Public repository:** [github.com/kaaan11/Wazuh-IRIS-SOC](https://github.com/kaaan11/Wazuh-IRIS-SOC)

The project began as a Wazuh-to-IRIS case integration and grew into a broader personal-lab
SOC workflow with enrichment, triage, detection rules, deduplication, routing, and
controlled response.

## What is implemented

The current public repository includes:

- Wazuh alert parsing and normalization
- IRIS Alert / Case routing by severity
- VirusTotal, Hybrid Analysis, and AbuseIPDB enrichment
- IOC and asset creation
- deduplication, recurrence counters, and severity escalation
- timeline updates for recurring alerts
- custom Wazuh rules for LOLBins, encoded PowerShell, persistence, and related behaviours
- FIM-triggered YARA response flow
- MITRE ATT&CK coverage tracking
- controlled response logic with fail-safe conditions

Several of these flows have been exercised against a live personal-lab Wazuh/Sysmon/IRIS
setup rather than existing only as static code.

## A design correction that mattered

The first version opened a Case for every eligible Wazuh alert. That turned the case list
into a raw alert queue.

The current design separates **Alert** from **Case**:

- lower-severity events enter the triage queue as Alerts
- higher-severity events can open investigation Cases directly

This better matches the way IRIS distinguishes triage from investigation.

## Safety boundary

Automated response is guarded by conservative controls. The default configuration keeps
response in dry-run mode, and the project records the distinction between a rule being
implemented and a response path being observed in the lab.

## What this does not prove

A validated personal-lab workflow is not the same thing as production-scale SOC
reliability. The project demonstrates engineering and investigation workflow design,
not enterprise deployment or operational SLA claims.

*Source status checked 2026-09-24.*
