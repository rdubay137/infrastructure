# ESXi Networking Configuration

## Date: 2026-03-26

## Environment
- Hypervisor: ESXi 8.0 U2
- Host NIC: Intel I226-V (2.5GbE)
- VM Network: Default "VM Network" Port Group

## Overview
This document outlines the networking configuration used to support virtual machines on the ESXi host, including connectivity required for DHCP and SSH access.

## Configuration Details

### vSwitch
- Default vSwitch (vSwitch0) used
- Connected to physical NIC (vmnic0)

### Port Group
- Name: VM Network
- VLAN: None (untagged)
- Used for all initial VM deployments

### VM Network Adapter
- Adapter Type: VMXNET3
- Connected at power on: Enabled
- Network: VM Network

## Observed Issue

- Ubuntu VM interface (ens34) was DOWN after installation
- No IP address assigned via DHCP
- Unable to reach external network or SSH into VM

## Root Cause

- ESXi networking was correctly configured
- Issue was within the guest OS (Ubuntu)
- Netplan configuration was missing

## Resolution

- Manually created netplan configuration file
- Enabled DHCP on interface ens34
- Brought interface UP
- Verified IP assignment (10.10.10.190)
- Confirmed SSH connectivity

## Validation Steps

- Verified interface state with `ip a`
- Confirmed IP address assignment
- Successfully established SSH session

## Key Takeaways

- ESXi network connectivity does not guarantee guest OS configuration
- VMXNET3 requires proper OS-level configuration
- Always validate both hypervisor and guest networking layers
- Troubleshooting requires isolating layers (hypervisor vs OS)
