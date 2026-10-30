# SOC Detection Lab Architecture

```mermaid
flowchart TD
    A["Windows 11 Endpoint"]
    B["Windows Security Logs"]
    C["Sysmon Event Logs"]
    D["PowerShell Script Block Logs"]
    E["Wazuh Agent"]
    F["Wazuh Manager - Docker"]
    G["Custom Detection Rules"]
    H["Wazuh Indexer - Docker"]
    I["Wazuh Dashboard - Docker"]

    A --> B
    A --> C
    A --> D
    B --> E
    C --> E
    D --> E
    E -->|"TCP 1514"| F
    G --> F
    F --> H
    H --> I
```

## Detection Rules
- 100100: Repeated Failed Logins
- 100101: Suspicious PowerShell Execution
- 100102: Unusual Parent-Child Process Behavior

## Technology Stack
- Windows 11
- Sysmon
- Windows Event Logging
- PowerShell Script Block Logging
- Wazuh Agent
- Wazuh Manager, Indexer, and Dashboard
- Docker Desktop

