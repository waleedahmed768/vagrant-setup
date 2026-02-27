# Vagrant Setup Guide

A complete guide to setting up and using Vagrant on Windows and Linux with support for multiple hypervisors: VirtualBox, VMware Workstation, and ESXi.

## Overview

This repository provides step-by-step instructions, configuration examples, and best practices for:
- Installing Vagrant on Windows and Linux
- Configuring Vagrant with VirtualBox
- Configuring Vagrant with VMware Workstation Pro/Player
- Provisioning VMs on ESXi using Vagrant
- Creating reusable Vagrantfiles for different scenarios

## Supported Platforms

- **Operating Systems**: Windows 10+, Windows Server, Linux (Ubuntu, CentOS, Debian)
- **Hypervisors**: 
  - VirtualBox (Free)
  - VMware Workstation Pro/Player
  - ESXi 6.0+

## Quick Links

- [Windows Installation Guide](./docs/windows-installation.md)
- [Linux Installation Guide](./docs/linux-installation.md)
- [VirtualBox Configuration](./docs/virtualbox-setup.md)
- [VMware Workstation Configuration](./docs/vmware-setup.md)
- [ESXi Configuration](./docs/esxi-setup.md)
- [Example Vagrantfiles](./examples/)

## Directory Structure

```
vagrant-setup/
├── README.md
├── docs/
│   ├── windows-installation.md
│   ├── linux-installation.md
│   ├── virtualbox-setup.md
│   ├── vmware-setup.md
│   └── esxi-setup.md
├── examples/
│   ├── basic-vm/
│   ├── multi-vm-cluster/
│   ├── ubuntu-server/
│   └── centos-server/
└── scripts/
    ├── install-vagrant-windows.ps1
    └── install-vagrant-linux.sh
```

## Prerequisites

- Administrator access on your machine
- Minimum 8GB RAM (16GB recommended)
- 20GB free disk space
- Internet connection for downloading images

## License

MIT License - See LICENSE file for details

## Contributing

Contributions are welcome! Please read CONTRIBUTING.md for guidelines.