# HQ VLAN Design

## 1. VLAN Overview

The HQ site currently uses three VLANs.

| VLAN ID | Subnet | Default Gateway |
|---|---|---|
| 10 | 192.168.10.0/29 | 192.168.10.1 |
| 20 | 192.168.20.0/29 | 192.168.20.1 |
| 30 | 192.168.30.0/29 | 192.168.30.1 |

No VLAN names are currently assigned.

## 2. End Devices

| Device | VLAN | IP Address | Default Gateway |
|---|---:|---|---|
| PC-HQ-01 | 30 | 192.168.30.2/29 | 192.168.30.1 |
| PC-HQ-02 | 10 | 192.168.10.3/29 | 192.168.10.1 |
| PC-HQ-03 | 10 | 192.168.10.2/29 | 192.168.10.1 |
| PC-HQ-04 | 20 | 192.168.20.2/29 | 192.168.20.1 |

IP addresses for end devices will be assigned during the implementation phase.

## 3. VLAN Gateway Design

The Layer 3 switch will provide the default gateway for each VLAN.

| VLAN | Gateway |
|---|---|
| 10 | 192.168.10.1 |
| 20 | 192.168.20.1 |
| 30 | 192.168.30.1 |

## 4. Transit Network

The L3 switch and HQ SRX are connected using a point-to-point /30 transit network.

| Device | IP Address |
|---|---|
| SRX-HQ-01 | 10.10.10.1/30 |
| L3-SW-HQ-01 | 10.10.10.2/30 |

Network: `10.10.10.0/30`

## 5. Design Notes

- VLANs 10, 20, and 30 are currently implemented in the HQ design.
- Inter-VLAN routing will be performed by the L3 switch.
- The L3 switch will use the SRX as its upstream device.
- The SRX will provide connectivity toward external networks.
- Additional VLANs may be introduced in future phases.