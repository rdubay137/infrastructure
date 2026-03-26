# Ubuntu VM Setup (doc-vm)

## Date: 2026-03-26

### Environment
- Hypervisor: ESXi 8.0 U2
- VM Name: doc-vm
- OS: Ubuntu Server 24.04 LTS

### Completed Tasks
- Configured ESXi networking
- Created Ubuntu VM
- Installed OS with OpenSSH
- Diagnosed network interface (ens34 DOWN)
- Created netplan configuration manually
- Enabled DHCP via netplan
- Brought interface UP (10.10.10.190)
- Established SSH access

### Key Issues & Resolutions
- NIC not active → required netplan config
- YAML indentation errors → corrected spacing
- Missing netplan file → created manually

### Lessons Learned
- ESXi NIC connection vs OS config are separate layers
- Netplan YAML is strict and unforgiving
- Always verify interface state with `ip a`
- SSH is critical for real workflow

### Commands Used
```bash
ip a
sudo nano /etc/netplan/01-netcfg.yaml
sudo netplan apply
ssh rdubay@10.10.10.190
```
