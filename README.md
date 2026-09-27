# SOC Home Lab

A practical Security Operations Center home lab built to develop hands-on experience in:

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

The lab is distributed across two physical systems:

### SOC / Analyst Side
- Laptop: Intel Core i7-11800H
- RAM: 16 GB
- VMware Workstation Pro
- Ubuntu Server 24.04 LTS
- Wazuh

### Enterprise / Attack Side
- Desktop: Ryzen 5 7600
- RAM: 32 GB
- VMware Workstation Pro

Planned systems:
- Windows Server Domain Controller
- Windows 11 endpoint
- Kali Linux attacker
- Linux server
- Suricata NDR sensor
- OPNsense firewall

## Current Progress

- [x] Created Ubuntu Server VM
- [x] Installed Ubuntu Server 24.04 LTS
- [x] Installed Wazuh Manager
- [x] Installed Wazuh Indexer
- [x] Installed Wazuh Dashboard
- [x] Verified Wazuh services
- [x] Accessed Wazuh dashboard from host
- [ ] Configure cross-device lab networking
- [ ] Deploy Windows Server Domain Controller
- [ ] Deploy Windows 11 endpoint
- [ ] Install Wazuh agents
- [ ] Install Sysmon
- [ ] Deploy Kali Linux
- [ ] Add Suricata
- [ ] Perform attack simulations
- [ ] Build detections
- [ ] Document investigations

## Disclaimer

This lab is intended for educational purposes in an isolated environment.
