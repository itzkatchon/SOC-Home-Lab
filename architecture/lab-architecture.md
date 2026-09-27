# SOC Home Lab Architecture

## Overview

The SOC home lab is distributed across two physical systems.

The laptop acts as the SOC and monitoring side, while the desktop acts as the simulated enterprise environment and attack platform.

The goal is to create a realistic environment where security telemetry is generated on the desktop side, forwarded to the SOC infrastructure, and then analyzed using SIEM, DFIR, and detection engineering tools.

## Physical Systems

### SOC Side - Laptop

- CPU: Intel Core i7-11800H
- RAM: 16 GB
- Host OS: Windows
- Hypervisor: VMware Workstation Pro

Primary role:

- Host the central SOC infrastructure
- Receive security telemetry
- Display and investigate alerts
- Support incident response and DFIR workflows
- Host the future SOC AI assistant backend

### Enterprise Side - Desktop

- CPU: AMD Ryzen 5 7600
- RAM: 32 GB
- Host OS: Windows
- Hypervisor: VMware Workstation Pro

Primary role:

- Simulate an enterprise environment
- Generate endpoint, identity, Linux, and network telemetry
- Provide systems for controlled attack simulation
- Host monitored endpoints and security sensors

## Current SOC-Side Architecture

```text
Laptop
|
+-- Windows Host
    |
    +-- VMware Workstation Pro
        |
        +-- SOC-WAZUH01
            |
            +-- Ubuntu Server 24.04 LTS
            +-- Wazuh Manager
            +-- Wazuh Indexer
            +-- Wazuh Dashboard
```

## Planned Enterprise-Side Architecture

```text
Desktop
|
+-- Windows Host
    |
    +-- VMware Workstation Pro
        |
        +-- DC01
        |   |
        |   +-- Windows Server 2022
        |   +-- Active Directory Domain Services
        |   +-- DNS
        |   +-- Wazuh Agent
        |
        +-- WIN11-01
        |   |
        |   +-- Windows 11
        |   +-- Domain-joined endpoint
        |   +-- Sysmon
        |   +-- Wazuh Agent
        |
        +-- KALI01
        |   |
        |   +-- Kali Linux
        |   +-- Controlled attack simulation
        |
        +-- LINUX-SRV01
        |   |
        |   +-- Ubuntu Server
        |   +-- SSH
        |   +-- Web server
        |   +-- auditd
        |   +-- Wazuh Agent
        |
        +-- NDR01
        |   |
        |   +-- Ubuntu Server
        |   +-- Suricata
        |   +-- Zeek later
        |
        +-- FIREWALL01
            |
            +-- OPNsense
            +-- Routing
            +-- Network segmentation
            +-- Firewall logging
```

## Full Lab Architecture

```text
                         Home Network
                              |
               +--------------+--------------+
               |                             |
            Laptop                        Desktop
         SOC / Analyst                Enterprise Lab
               |                             |
        SOC-WAZUH01                 +---------+---------+
               |                    |         |         |
          Wazuh Server             DC01    WIN11-01   KALI01
               |                    |         |         |
               |                    |         |         |
               |                 AD / DNS   Sysmon    Attacks
               |                    |         |         |
               |                    +----+----+         |
               |                         |              |
               |                     Telemetry          |
               |                         |              |
               |                         +--------------+
               |                              |
               |                         LINUX-SRV01
               |                              |
               |                            Logs
               |                              |
               |                            NDR01
               |                         Suricata / Zeek
               |                              |
               +----------- Telemetry --------+
                              |
                              v
                           Wazuh
                              |
                              v
                         SOC Analyst
```

## Monitoring Flow

```text
Endpoints and Servers
        |
        v
Windows Event Logs / Sysmon / Linux Logs
        |
        v
Wazuh Agents
        |
        v
Wazuh Manager
        |
        v
Wazuh Indexer
        |
        v
Wazuh Dashboard
        |
        v
SOC Investigation
```

## Network Detection Flow

```text
KALI01
   |
   | Controlled attack traffic
   v
WIN11-01 / DC01 / LINUX-SRV01
   |
   v
NDR01
   |
   +-- Suricata
   +-- Zeek
   |
   v
Network telemetry
   |
   v
Wazuh
```

## Incident Investigation Flow

```text
Attack
  |
  v
Security Event
  |
  v
Endpoint / Network Telemetry
  |
  v
Wazuh Detection
  |
  v
SOC Alert
  |
  v
Analyst Investigation
  |
  +-- Event correlation
  +-- Timeline analysis
  +-- MITRE ATT&CK mapping
  +-- True Positive / False Positive decision
  +-- Incident documentation
```

## Future SOC AI Integration

The SOC AI assistant is planned to integrate with the SIEM environment rather than operate only on static or synthetic data.

The intended workflow is:

```text
Wazuh Alert
    |
    v
SOC AI Assistant
    |
    +-- Retrieve related events
    +-- Correlate evidence
    +-- Build incident timeline
    +-- Generate 5W triage
    +-- Map activity to MITRE ATT&CK
    +-- Reference supporting evidence
    +-- Assign confidence
    |
    v
Human Analyst
    |
    +-- True Positive
    +-- False Positive
    +-- Needs Investigation
```

The goal is to keep the analyst in the decision-making loop while using the AI assistant to accelerate triage and evidence correlation.

## Planned Tools

### SIEM and Monitoring

- Wazuh
- Splunk later

### Endpoint Telemetry

- Sysmon
- Windows Event Logs
- Linux audit logs

### Network Detection

- Suricata
- Zeek

### DFIR

- Wireshark
- KAPE
- Eric Zimmerman tools
- Volatility
- Velociraptor
- Hayabusa
- Chainsaw

### Detection Engineering

- Sigma
- Wazuh rules
- SPL later
- YARA later

### Attack Simulation

- Kali Linux
- Atomic Red Team
- Controlled manual attack simulations

## Current Status

- [x] SOC-WAZUH01 deployed
- [x] Ubuntu Server configured
- [x] Wazuh Manager installed
- [x] Wazuh Indexer installed
- [x] Wazuh Dashboard installed
- [x] Wazuh services validated
- [x] Wazuh dashboard accessible from the host
- [ ] Configure laptop-to-desktop connectivity
- [ ] Deploy DC01
- [ ] Deploy WIN11-01
- [ ] Configure Active Directory
- [ ] Install Wazuh agents
- [ ] Install Sysmon
- [ ] Deploy KALI01
- [ ] Deploy NDR01
- [ ] Configure Suricata
- [ ] Begin attack and investigation exercises
- [ ] Integrate SOC AI assistant
