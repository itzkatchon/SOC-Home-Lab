# SOC Home Lab

A practical Security Operations Center home lab designed to build hands-on experience in:

- SIEM monitoring
- Endpoint telemetry
- Detection engineering
- Incident response
- Digital forensics
- Network detection
- Active Directory security
- MITRE ATT&CK mapping
- Attack simulation

## Lab Architecture

The lab is distributed across two physical systems.

### SOC / Analyst Side

- Laptop: Intel Core i7-11800H
- RAM: 16 GB
- Host OS: Windows
- Hypervisor: VMware Workstation Pro
- SOC VM: Ubuntu Server 24.04 LTS
- SIEM: Wazuh

Current SOC components:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

### Enterprise / Attack Side

- Desktop: AMD Ryzen 5 7600
- RAM: 32 GB
- Host OS: Windows
- Hypervisor: VMware Workstation Pro

Current enterprise systems:

- `DC01`
  - Windows Server 2022
  - Active Directory Domain Services
  - DNS Server
  - Domain: `soclab.local`

Planned systems:

- `WIN11-01` Windows endpoint
- `KALI01` attacker system
- Linux server
- Suricata NDR sensor
- OPNsense firewall

## Current Architecture

```text
                          Home Network
                               |
                +--------------+--------------+
                |                             |
             Laptop                        Desktop
          SOC / Analyst                Enterprise Lab
                |                             |
        SOC-WAZUH01                        DC01
                |                             |
      Ubuntu Server 24.04              Windows Server 2022
                |                             |
        +-------+-------+              +------+------+
        |       |       |              |             |
      Wazuh   Wazuh   Wazuh       Active Directory  DNS
      Manager Indexer Dashboard          |
                                         |
                                   soclab.local
```

## Documentation

- [Wazuh SOC Server Deployment](setup/01-soc-laptop-wazuh.md)
- [Windows Server Domain Controller Deployment](setup/02-dc01.md)
- [Lab Architecture](architecture/lab-architecture.md)

## Current Progress

### SOC Infrastructure

- [x] Create Ubuntu Server VM
- [x] Install Ubuntu Server 24.04 LTS
- [x] Install Wazuh Manager
- [x] Install Wazuh Indexer
- [x] Install Wazuh Dashboard
- [x] Verify Wazuh services
- [x] Access Wazuh dashboard from the Windows host

### Enterprise Infrastructure

- [x] Deploy Windows Server 2022
- [x] Rename server to `DC01`
- [x] Install Active Directory Domain Services
- [x] Install DNS Server
- [x] Create the `soclab.local` Active Directory forest
- [x] Validate the domain configuration
- [ ] Create Active Directory organizational units
- [ ] Create lab users and groups
- [ ] Deploy `WIN11-01`
- [ ] Join `WIN11-01` to `soclab.local`

### Monitoring and Detection

- [ ] Configure cross-device networking
- [ ] Install Wazuh agent on `DC01`
- [ ] Install Wazuh agent on `WIN11-01`
- [ ] Install Sysmon
- [ ] Configure Windows audit policies
- [ ] Forward Windows telemetry to Wazuh
- [ ] Deploy Suricata
- [ ] Add Splunk

### Attack Simulation and Investigation

- [ ] Deploy Kali Linux
- [ ] Configure Atomic Red Team
- [ ] Perform controlled attack simulations
- [ ] Build detection rules
- [ ] Perform SOC investigations
- [ ] Map activity to MITRE ATT&CK
- [ ] Document incident findings

## Planned Detection and Investigation Workflow

```text
Attack Simulation
       |
       v
Enterprise Endpoint
       |
       v
Windows / Sysmon / Network Telemetry
       |
       v
Wazuh
       |
       v
Detection
       |
       v
SOC Investigation
       |
       +-- Event correlation
       +-- Timeline analysis
       +-- MITRE ATT&CK mapping
       +-- True Positive / False Positive classification
       +-- Incident documentation
```

## Future Development

The lab will later be extended with:

- Sysmon-based endpoint telemetry
- Suricata network detection
- Splunk SIEM practice
- Velociraptor and DFIR tooling
- Sigma detection rules
- Atomic Red Team attack simulation
- SOC AI assistant integration with Wazuh

## Disclaimer

This lab is intended strictly for educational and defensive security purposes in an isolated environment.
