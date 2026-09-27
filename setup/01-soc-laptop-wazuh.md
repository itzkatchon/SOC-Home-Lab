# 01 - SOC Laptop and Wazuh Deployment

## Objective

The first phase of the SOC home lab establishes the central monitoring infrastructure.

The laptop acts as the SOC-side system and hosts the Wazuh server inside VMware Workstation Pro.

## Host Hardware

- CPU: Intel Core i7-11800H
- RAM: 16 GB
- Host OS: Windows
- Hypervisor: VMware Workstation Pro

## Virtual Machine

### SOC-WAZUH01

- Operating System: Ubuntu Server 24.04 LTS
- vCPU: 4
- RAM: 8 GB
- Disk: 80 GB
- Initial Network Mode: NAT
- Hostname: `soc-wazuh01`

## Installed Components

The Wazuh all-in-one deployment includes:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

## Ubuntu Preparation

The server was updated before installing Wazuh:

```bash
sudo apt update
sudo apt upgrade -y
```

OpenSSH Server was also enabled to allow remote administration from the Windows host.

## Wazuh Installation

The Wazuh installation script was downloaded using:

```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
```

The all-in-one deployment was installed using:

```bash
sudo bash ./wazuh-install.sh -a
```

This installed the following components on the same Ubuntu server:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

## Service Validation

After installation and reboot, the Wazuh services were verified using:

```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
```

All three services were confirmed to be active and running.

## Dashboard Access

The Wazuh dashboard was accessed from the Windows host using the Ubuntu VM's IP address over HTTPS.

Example:

```text
https://<WAZUH-SERVER-IP>
```

The browser initially displayed a certificate warning because the Wazuh deployment uses a self-signed certificate.

After continuing to the site, the Wazuh dashboard was successfully accessed using the administrator account created during installation.

## Current Architecture

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

## Role of the Laptop

The laptop is used as the SOC and monitoring side of the home lab.

Its primary responsibilities will include:

- Receiving security telemetry from lab endpoints
- Storing and indexing security events
- Generating and displaying alerts
- Supporting incident investigation
- Acting as the backend for future SOC AI integration
- Providing the analyst interface through the Wazuh dashboard

The physical Windows host is also used for administrative and analyst tasks such as accessing the Wazuh dashboard and connecting to the Ubuntu server through SSH.

## Result

The central Wazuh SIEM infrastructure is operational.

The Ubuntu server boots successfully, the Wazuh services start automatically, and the Wazuh dashboard is accessible from the Windows host.

The environment is now ready to receive telemetry from systems that will be deployed on the desktop side of the SOC home lab.

## Next Steps

- Configure networking between the laptop and desktop
- Ensure the desktop can reach the Wazuh server
- Deploy the Windows Server domain controller
- Configure Active Directory and DNS
- Deploy a Windows 11 endpoint
- Join the Windows endpoint to the domain
- Install Wazuh agents
- Install Sysmon
- Configure Windows logging and audit policies
- Deploy Kali Linux for controlled attack simulation
- Add Suricata for network detection
- Begin generating and investigating security events
- Document detections and investigations in the repository
