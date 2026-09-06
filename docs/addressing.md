# HQ IP Addressing Plan

## 1. VLAN Networks

| VLAN | Network | Usable Range | Gateway | Broadcast |
|---|---|---|---|---|
| 10 | 192.168.10.0/29 | 192.168.10.1 - 192.168.10.6 | 192.168.10.1 | 192.168.10.7 |
| 20 | 192.168.20.0/29 | 192.168.20.1 - 192.168.20.6 | 192.168.20.1 | 192.168.20.7 |
| 30 | 192.168.30.0/29 | 192.168.30.1 - 192.168.30.6 | 192.168.30.1 | 192.168.30.7 |

## 2. End Devices

| Device | VLAN | IP Address | Default Gateway |
|---|---:|---|---|
| PC-HQ-01 | 30 | 192.168.30.2/29 | 192.168.30.1 |
| PC-HQ-02 | 10 | 192.168.10.3/29 | 192.168.10.1 |
| PC-HQ-03 | 10 | 192.168.10.2/29 | 192.168.10.1 |
| PC-HQ-04 | 20 | 192.168.20.2/29 | 192.168.20.1 |

## 3. Firewall-to-Switch Transit

| Device | Interface Role | IP Address |
|---|---|---|
| SRX-HQ-01 | Transit | 10.10.10.1/30 |
| L3-SW-HQ-01 | Transit | 10.10.10.2/30 |

Network: `10.10.10.0/30`

## 4. Addressing Strategy

The HQ VLANs use /29 networks to provide a small address space suitable for the current lab topology.

Additional addresses remain available within each subnet for future lab devices.