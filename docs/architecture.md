# HQ Network Architecture

## 1. Overview

This project represents the network infrastructure of the HQ site.

The current topology consists of:

- One Juniper SRX firewall
- One Layer 3 switch
- One Layer 2 access switch
- Four end devices

The design will be expanded in later phases to include Layer 2
security, VRRP, SRX high availability, and HQ-to-Branch IPsec VPN.

---

## 2. Current Topology

```text
                      HQ
                       |
                    [ SRX ]
                       |
                 [ L3 Switch ]
                 /      |      \
               /        |       \
              |        PC2      PC1 
             |                   
      [ L2 Access Switch ]
       /           \
      PC3          PC4


3. Device Roles
Device	Role	Function
SRX-HQ-01	Firewall	Security boundary, routing, NAT, security policies
L3-SW-HQ-01	Layer 3 Switch	VLANs, SVIs, inter-VLAN routing
L2-SW-HQ-01	Access Switch	Layer 2 connectivity and VLAN access
PC-HQ-01	End Device	User endpoint
PC-HQ-02	End Device	User endpoint
PC-HQ-03	End Device	User endpoint
PC-HQ-04	End Device	User endpoint


4. Physical Connectivity
Device A	Interface	Device B	Interface	Link Type
SRX-HQ-01	TBD	L3-SW-HQ-01	TBD	TBD
L3-SW-HQ-01	TBD	L2-SW-HQ-01	TBD	Trunk
L3-SW-HQ-01	TBD	PC-HQ-01	TBD	Access
L3-SW-HQ-01	TBD	PC-HQ-02	TBD	Access
L2-SW-HQ-01	TBD	PC-HQ-03	TBD	Access
L2-SW-HQ-01	TBD	PC-HQ-04	TBD	Access


5. Network Responsibilities
SRX-HQ-01

The SRX will provide:

Security zones
Security policies
NAT
External connectivity
Routing toward external networks
L3-SW-HQ-01

The Layer 3 switch will provide:

VLANs
SVIs
Inter-VLAN routing
Default gateway functionality
Routing toward the SRX
L2-SW-HQ-01

The access switch will provide:

VLAN assignment
Access ports
Trunk connectivity toward the L3 switch


6. Future Enhancements

The current topology is intentionally kept simple.

Future project phases may introduce:

VRRP
Layer 2 security
SRX Chassis Cluster
Redundant links
Firewall failover
Additional network segments
HQ-to-Branch connectivity
Site-to-site IPsec VPN

