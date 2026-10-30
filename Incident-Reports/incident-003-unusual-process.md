# SOC Incident Report 003: Unusual Parent-Child Process Behavior

## Incident Summary
On October 29, 2026, Wazuh detected an unusual parent-child process relationship on SOC-LAB-WIN11.

A custom-built executable named WINWORD.EXE launched Windows PowerShell. Custom detection rule 100102 generated a Level 10 alert.

The activity was intentionally simulated during authorized SOC laboratory testing. The parent executable was not the genuine Microsoft Word application.

## Detection Information
- Custom Rule ID: 100102
- Severity: Level 10
- Endpoint: SOC-LAB-WIN11
- Windows Event ID: 1
- Telemetry Source: Sysmon
- MITRE ATT&CK: T1059.001 - PowerShell
- MITRE Tactic: Execution

## Investigation Timeline
Date: October 29, 2026

- 22:08:16 - Sysmon recorded a PowerShell process creation event.
- 22:08:17.456 - Wazuh recorded the custom Rule 100102 alert.

## Technical Findings
Parent executable:
C:\SOC-Lab\Process-Test\WINWORD.EXE

Child executable:
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe

Observed command:
powershell.exe -NoProfile -Command "Write-Output SOC-LAB-PROCESS-TEST"

- Parent process ID: 25732
- Child process ID: 11504
- Integrity level: High
- The child process printed a harmless test string.
- The unusual process relationship matched the custom detection.

## Analyst Assessment
Office applications launching scripting engines may indicate suspicious execution activity. In this case, the parent executable was a purpose-built laboratory simulation rather than the real Microsoft Word program.

The observed PowerShell command was benign. The evidence supports a successful custom detection test, not an actual compromise.

## Disposition
Authorized Security Testing - No Confirmed Compromise

## Lessons Learned
- Sysmon Event ID 1 records process creation activity.
- Parent-child process relationships provide important investigation context.
- Process names alone do not prove application identity.
- Command-line analysis helps distinguish benign testing from suspicious behavior.
- MITRE ATT&CK mapping provides standardized technique classification.

## Evidence
- phase4-process-parent-child.png
- phase4-process-sysmon-event.png
- Wazuh Rule 100102 alert
- Sysmon Event ID 1
