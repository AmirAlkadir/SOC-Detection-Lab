# SOC Detection & Threat Investigation Lab

A hands-on cybersecurity project using Wazuh, Sysmon, and Windows event logging to develop, test, and investigate custom security detections.

## Project Overview

Built a Windows 11 endpoint monitoring environment using a Wazuh SIEM deployment hosted in Docker. Configured Sysmon and PowerShell Script Block Logging to collect process, authentication, and script execution telemetry.

Developed three custom Wazuh detection rules, conducted controlled simulations, investigated generated alerts, and documented findings in incident reports.

## Technology Stack

- Wazuh SIEM (Manager, Indexer, Dashboard)
- Docker Desktop
- Windows 11
- Sysmon
- Windows Security Event Logs
- PowerShell Script Block Logging
- PowerShell
- MITRE ATT&CK

## Architecture

See [SOC Lab Architecture](Architecture/architecture.md).

The Windows endpoint collects security telemetry through the Wazuh agent. Events are analyzed by the Wazuh manager, and matching alerts are indexed and reviewed in the dashboard.

## Custom Detection Rules

| Rule ID | Detection | Severity | MITRE ATT&CK |
|---|---|---|---|
| 100100 | Repeated Failed Login Attempts | 10 | T1110 |
| 100101 | Suspicious PowerShell Execution | 8 | T1059.001 |
| 100102 | Unusual Parent-Child Process Behavior | 10 | T1059.001 |

### Detection 1: Repeated Failed Logins

Developed a correlation rule for repeated Windows Event ID 4625 authentication failures within a 60-second window.

Improved the detection by correlating failures targeting the same username, reducing unrelated-account correlation.

[View detection rule](Detection-Rules/failed-login-rule.xml)

### Detection 2: Suspicious PowerShell

Developed a custom rule analyzing PowerShell Script Block Logging (Event ID 4104) for Invoke-Expression and IEX execution patterns.

Validated detection using harmless PowerShell commands and confirmed that basic commands did not produce matching alerts.

[View detection rule](Detection-Rules/suspicious-powershell-rule.xml)

### Detection 3: Unusual Process Behavior

Developed a Sysmon Event ID 1 rule to detect a WINWORD.EXE process launching PowerShell.

Validated the rule using a harmless executable named WINWORD.EXE. This was a filename-based simulation, not genuine Microsoft Word execution.

[View detection rule](Detection-Rules/unusual-process-rule.xml)

## Incident Investigations

Three controlled security investigations were documented:

1. [Repeated Failed Login Investigation](Incident-Reports/incident-001-failed-logins.md)
2. [Suspicious PowerShell Investigation](Incident-Reports/incident-002-suspicious-powershell.md)
3. [Unusual Process Behavior Investigation](Incident-Reports/incident-003-unusual-process.md)

Each report covers detection details, technical evidence, investigation findings, and analyst assessment.

## Detection Testing and Tuning

- Successfully triggered all three custom detections.
- Tested benign activity against each detection.
- Tuned failed-login correlation to match the same target username.
- Verified individual failed-login events could be detected without triggering the repeated-login rule.
- Investigated and restored a disconnected Wazuh agent after identifying manager process-state issues.

Testing was conducted in a controlled laboratory. Negative-test results are limited to the specific scenarios exercised and do not constitute a comprehensive false-positive measurement.

## Evidence

Screenshots of endpoint telemetry, detection alerts, and investigation findings were captured during testing. Selected redacted evidence will be added after privacy review.

## Key Skills Demonstrated

- SIEM deployment and administration
- Windows security event analysis
- Sysmon telemetry collection
- Detection engineering and custom Wazuh XML rules
- PowerShell activity monitoring
- Security event correlation
- MITRE ATT&CK mapping
- Alert triage and investigation
- False-positive testing and detection tuning
- Technical incident documentation

## Disclaimer

All simulations were conducted in an authorized local laboratory environment. The project does not demonstrate unauthorized access or actual compromise.

