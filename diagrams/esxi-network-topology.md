# ESXi Network Topology

## Overview
This diagram represents the relationship between the physical network, ESXi host, virtual switch, and Ubuntu VM.

## Topology Diagram

```
[ Physical Network / Router ]
            |
        (vmnic0)
            |
      [ ESXi Host ]
            |
        [ vSwitch0 ]
            |
     [ Port Group: VM Network ]
            |
      [ Ubuntu VM (doc-vm) ]
            |
        Interface: ens34
            |
     IP: 10.10.10.190 (DHCP)
```

## Notes
- Physical NIC (vmnic0) connects ESXi to the network
- vSwitch0 bridges physical and virtual networking
- VM Network port group provides connectivity to VMs
- Ubuntu VM receives IP via DHCP
- ens34 is the VM’s network interface mapped to VMXNET3

## Key Insight
Even when ESXi networking is correctly configured, the guest OS must still configure its own interface (netplan in Ubuntu).
