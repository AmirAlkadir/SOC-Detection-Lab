# SOC Incident Report 001: Repeated Failed Login Attempts

## Incident Summary
On October 29, 2026, Wazuh detected a cluster of failed Windows authentication attempts on the SOC-LAB-WIN11 endpoint. Custom detection rule 100100 generated a Level 10 alert after repeated authentication failures targeting SOC-LAB-TEST-USER.

The activity was generated through authorized testing in a controlled SOC laboratory.

## Detection Information
- Detection: Repeated Windows Failed Login Attempts
- Custom Rule ID: 100100
- Severity: Level 10
- Endpoint: SOC-LAB-WIN11
- Windows Event ID: 4625
- Underlying Wazuh Rule: 60122
- MITRE ATT&CK: T1110 - Brute Force

## Investigation Timeline
Date: October 29, 2026

- 21:34:54.135 - Failed authentication event recorded.
- 21:34:54.137 - Additional failed authentication event recorded.
- 21:34:55.256 - Failed authentication event recorded.
- 21:34:55.258 - Additional failed authentication event recorded.
- 21:34:55.260 - Custom Wazuh rule 100100 generated a Level 10 alert.
- 21:34:55.263 - Another underlying failed-login alert was indexed.

## Technical Findings
- Target account: SOC-LAB-TEST-USER
- Source IP: ::1 (IPv6 loopback)
- Logon type: 2 (Interactive)
- Failure status: 0xC000006D
- Failure substatus: 0xC0000064 (Unknown username)
- Five underlying Rule 60122 alerts were identified within approximately 1.1 seconds.
- No matching successful-login alerts were found in the Wazuh alert index during the reviewed period.

## Analyst Assessment
The authentication failures were generated intentionally as part of authorized SOC detection testing. The activity originated locally and targeted a nonexistent test username.

The available alert evidence does not establish a successful account compromise. The absence of successful-login alerts is not definitive proof that no successful authentication occurred.

## Disposition
Authorized Security Testing - No Confirmed Compromise

## Lessons Learned
- Correlation rules can identify rapid repeated authentication failures.
- Username-based correlation reduces alerts caused by failures across unrelated usernames.
- Investigating individual Windows Event ID 4625 records provides context beyond the aggregate detection.
- Wazuh alert searches must be interpreted with awareness of event filtering and retention.

## Evidence
- phase4-failed-login-timeline.png
- Wazuh custom Rule 100100 alert screenshots
- Windows Security Event ID 4625 records
