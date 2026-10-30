# SOC Incident Report 002: Suspicious PowerShell Execution

## Incident Summary
On October 29, 2026, Wazuh detected dynamic PowerShell execution on the SOC-LAB-WIN11 endpoint. Custom rule 100101 generated a Level 8 alert after detecting Invoke-Expression in a PowerShell script block.

The activity was intentionally generated during authorized SOC laboratory testing.

## Detection Information
- Custom Rule ID: 100101
- Severity: Level 8
- Endpoint: SOC-LAB-WIN11
- Windows Event ID: 4104
- Event Channel: Microsoft-Windows-PowerShell/Operational
- MITRE ATT&CK: T1059.001 - PowerShell

## Investigation Timeline
Date: October 29, 2026

- 21:47:42 - PowerShell script block event generated.
- 21:47:43.007 - Wazuh indexed the custom Level 8 alert.

## Technical Findings
- Script Block ID: 395030ac-7992-4a52-b3f2-dfb7f1ad62f1
- Process ID: 24908
- Recorded command:

  Invoke-Expression 'Write-Output "SOC-LAB-POWERSHELL-DETECTION-TEST"'

- Invoke-Expression dynamically evaluates and executes PowerShell code.
- The observed payload only printed a harmless test string.
- One PowerShell-channel alert was found in the reviewed Wazuh alert results.

## Analyst Assessment
Dynamic PowerShell execution is a useful detection indicator because it can be abused by attackers. However, the specific script block captured during this investigation contained no observed malicious payload.

The event was generated intentionally as part of authorized SOC detection testing. No compromise was established from the available evidence.

## Disposition
Authorized Security Testing - No Confirmed Compromise

## Lessons Learned
- PowerShell Script Block Logging provides visibility into executed script content.
- Wazuh can correlate PowerShell telemetry with custom detection rules.
- Suspicious commands require contextual investigation before being classified as malicious.
- MITRE ATT&CK mapping provides a framework for describing observed techniques.

## Evidence
- phase4-powershell-scriptblock.png
- phase4-powershell-alert-details.png
- Wazuh Rule 100101 alert
- Windows PowerShell Event ID 4104
