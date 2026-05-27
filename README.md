# Hyper-V Lab Environment Setup Guide

Complete guide to building and configuring a comprehensive Hyper-V lab environment with Windows 11, Windows Server 2025, pfSense, Ubuntu Desktop, Ubuntu Server, and Kali Linux.

## Table of Contents

1. [Overview](#overview)
2. [Lab Components](#lab-components)
3. [Host Requirements](#host-requirements)
4. [Network Architecture](#network-architecture)
5. [Quick Start](#quick-start)
6. [Detailed Guides](#detailed-guides)
7. [Automation Scripts](#automation-scripts)
8. [Troubleshooting](#troubleshooting)

## Overview

This lab environment provides a comprehensive learning and testing platform for:
- Windows ecosystem administration and security
- Linux system administration
- Network security and firewall management
- Penetration testing and cybersecurity training
- Active Directory and domain management

## Lab Components

| Component | Purpose | Guide |
|-----------|---------|-------|
| **Windows 11** | Client OS, AD joined machine | [Windows 11 Setup](./docs/windows-11-setup.md) |
| **Windows Server 2025** | Domain controller, file server, infrastructure | [Windows Server 2025 Setup](./docs/windows-server-2025-setup.md) |
| **pfSense** | Firewall, router, network security | [pfSense Setup](./docs/pfsense-setup.md) |
| **Ubuntu Desktop** | Linux workstation, development | [Ubuntu Desktop Setup](./docs/ubuntu-desktop-setup.md) |
| **Ubuntu Server** | Linux server, services, testing | [Ubuntu Server Setup](./docs/ubuntu-server-setup.md) |
| **Kali Linux** | Penetration testing, security tools | [Kali Linux Setup](./docs/kali-linux-setup.md) |

## Host Requirements

### Minimum Requirements
- **CPU**: 8 cores (Intel/AMD)
- **RAM**: 32 GB (64 GB recommended)
- **Storage**: 500 GB SSD (1 TB+ recommended)
- **Hyper-V Support**: CPU with virtualization extensions enabled

### Recommended Requirements
- **CPU**: 16+ cores
- **RAM**: 64 GB or more
- **Storage**: 2 TB SSD (NVMe preferred)
- **Network**: Gigabit Ethernet or better

## Network Architecture

```
┌─────────────────────────────────────────────────────┐
│                   Host Network                       │
│              (192.168.1.0/24 - NAT)                 │
└──────────────���──────────────────────────────────────┘
                        │
        ┌───────────────┴───────────────┐
        │                               │
    ┌───────────┐              ┌────────────────┐
    │  pfSense  │              │  vSwitch: Lab  │
    │  Router   │              │  (Internal)    │
    │192.168.100│              │10.0.0.0/24     │
    │    .1     │              └────────────────┘
    └───────────┘                      │
        │         ┌────────────────────┼────────────┐
        │         │                    │            │
    ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
    │Windows 11│ │Windows   │ │ Ubuntu   │ │ Ubuntu   │
    │10.0.0.10 │ │ Server   │ │ Desktop  │ │ Server   │
    │          │ │ 2025     │ │ 10.0.0.30│ │ 10.0.0.40│
    │          │ │ 10.0.0.20��� │          │ │          │
    └──────────┘ └──────────┘ └──────────┘ └──────────┘
    
    ┌──────────┐
    │ Kali     │
    │ Linux    │
    │10.0.0.50 │
    └──────────┘
```

## Quick Start

### 1. Enable Hyper-V
```powershell
# Run as Administrator
Enable-WindowsOptionalFeature -FeatureName Microsoft-Hyper-V -All -Online
```

### 2. Create Virtual Switch
See [Network Configuration Guide](./docs/network-setup.md)

### 3. Create and Configure VMs
Follow the component-specific guides in the [Detailed Guides](#detailed-guides) section

### 4. Run Automation Scripts
See [Automation Scripts](#automation-scripts) section

## Detailed Guides

- [Windows 11 Setup Guide](./docs/windows-11-setup.md)
- [Windows Server 2025 Setup Guide](./docs/windows-server-2025-setup.md)
- [pfSense Setup Guide](./docs/pfsense-setup.md)
- [Ubuntu Desktop Setup Guide](./docs/ubuntu-desktop-setup.md)
- [Ubuntu Server Setup Guide](./docs/ubuntu-server-setup.md)
- [Kali Linux Setup Guide](./docs/kali-linux-setup.md)
- [Network Configuration](./docs/network-setup.md)

## Automation Scripts

Automated setup scripts are available in the `scripts/` directory:

- `setup-hyper-v-host.ps1` - Configure Hyper-V host
- `create-vms.ps1` - Batch create all VMs
- `configure-network.ps1` - Setup network infrastructure
- `deploy-windows-11.ps1` - Automated Windows 11 setup
- `deploy-windows-server-2025.ps1` - Automated WS2025 setup
- `deploy-ubuntu.ps1` - Automated Ubuntu deployment
- `deploy-kali.ps1` - Automated Kali deployment

## Troubleshooting

See [Troubleshooting Guide](./docs/troubleshooting.md) for common issues and solutions.

## Directory Structure

```
hyper-v-lab-environment-/
├── README.md
├── docs/
│   ├── windows-11-setup.md
│   ├── windows-server-2025-setup.md
│   ├── pfsense-setup.md
│   ├── ubuntu-desktop-setup.md
│   ├── ubuntu-server-setup.md
│   ├── kali-linux-setup.md
│   ├── network-setup.md
│   └── troubleshooting.md
├── scripts/
│   ├── setup-hyper-v-host.ps1
│   ├── create-vms.ps1
│   ├── configure-network.ps1
│   ├── deploy-windows-11.ps1
│   ├── deploy-windows-server-2025.ps1
│   ├── deploy-ubuntu.ps1
│   └── deploy-kali.ps1
└── configs/
    ├── pfsense-config.xml
    ├── windows-server-config.xml
    └── network-config.json
```

## Getting Started

1. Ensure your Hyper-V host meets the [requirements](#host-requirements)
2. Review the [network architecture](#network-architecture)
3. Follow the [quick start](#quick-start) guide
4. Work through each component's detailed guide
5. Use automation scripts to speed up deployment
6. Refer to troubleshooting guide if issues arise

## Contributing

Feel free to contribute improvements, fixes, and additional documentation.

## License

This project is provided as-is for educational and professional use.

---

**Last Updated**: 2026-05-27
