# Enterprise HQ Network Lab

A hands-on enterprise network lab built to simulate a small HQ environment using a Juniper SRX firewall, Layer 3 switching, VLAN segmentation, and static routing.

The project focuses on practical configuration, verification, troubleshooting, and documenting the behavior of the network.

---

## 1. Topology

![Enterprise HQ Network Topology](docs/images/Enterprise-HQ-Topology.svg)

The HQ site consists of:

* Juniper SRX firewall
* One Layer 3 switch
* One Layer 2 switch
* Four end devices


```

The Layer 3 switch also provides the VLAN gateways and performs inter-VLAN routing.

---

## 2. Addressing

### HQ-SRX

| Interface | Address       | Purpose                |
| --------- | ------------- | ---------------------- |
| ge-0/0/0  | 10.10.10.1/30 | Connection to L3-SW-HQ |

### L3-SW-HQ

| Interface   | Address       | Purpose              |
| ----------- | ------------- | -------------------- |
| Ethernet0/0 | 10.10.10.2/30 | Connection to HQ-SRX |

### VLANs

| VLAN    | Network         | Gateway      |
| ------- | --------------- | ------------ |
| VLAN 10 | 192.168.10.0/29 | 192.168.10.1 |
| VLAN 20 | 192.168.20.0/29 | 192.168.20.1 |
| VLAN 30 | 192.168.30.0/29 | 192.168.30.1 |

The VLAN gateways are configured on the Layer 3 switch.

---

## 3. Network Architecture

Traffic between the internal VLANs is routed by L3-SW-HQ.

Traffic leaving the internal network toward the SRX is forwarded using the Layer 3 switch default route:

```text
0.0.0.0/0 → 10.10.10.1
```

The SRX provides the boundary between the internal network and the external/upper network.

---

## 4. VLAN Segmentation

Three VLANs are used to separate internal network segments:

```text
VLAN 10 → 192.168.10.0/29
VLAN 20 → 192.168.20.0/29
VLAN 30 → 192.168.30.0/29
```

The Layer 3 switch provides the corresponding SVI gateways.

This allows the lab to demonstrate:

* VLAN segmentation
* Access ports
* Trunk connectivity
* Inter-VLAN routing
* Layer 3 forwarding

---

## 5. Routing

The L3 switch uses the SRX as its default next hop:

```text
0.0.0.0/0 → 10.10.10.1
```

The SRX has routes toward the internal VLAN networks through L3-SW-HQ.

Example:

```text
192.168.10.0/29 → 10.10.10.2
192.168.20.0/29 → 10.10.10.2
192.168.30.0/29 → 10.10.10.2
```

---

## 6. SRX Security

The SRX is configured with the internal interface connected to the Layer 3 switch.

Security zones and policies are used to control traffic through the firewall.

The lab focuses on understanding how traffic moves between:

```text
Internal VLANs
      ↓
L3-SW-HQ
      ↓
HQ-SRX
      ↓
External Network
```

---

## 7. Connectivity Verification

Connectivity was verified between the end devices, VLAN gateways, Layer 3 switch, and SRX.

The verification included:

* End device to gateway connectivity
* VLAN-to-VLAN communication
* L3-SW-HQ to SRX connectivity
* End-to-end connectivity through the network
* Testing after interface state changes

The tests confirmed that the VLANs, Layer 3 routing, and SRX connectivity were operating as expected.

---

## 8. Interface Failure Testing

The lab was also used to test interface behavior.

For example, shutting down the VLAN 30 interface resulted in the device connected to that VLAN losing connectivity to the SRX.

Restoring the interface with:

```text
no shutdown
```

restored connectivity.

This provided a simple operational test demonstrating how an interface state change affects network reachability.

---

## 9. Project Structure

```text
enterprise-hq/
│
├── README.md
├── configs/
├── docs/
├── testing/
└── troubleshooting/
```

Additional documentation can be added as the lab evolves.

---

## 10. Technologies

* Juniper SRX
* Junos OS
* Cisco Layer 3 Switching
* Cisco Layer 2 Switching
* VLANs
* 802.1Q Trunking
* Inter-VLAN Routing
* Static Routing
* Security Zones
* Security Policies
* Network Troubleshooting

---

## 11. Future Development

This HQ environment is intended to become part of a larger enterprise networking project.

Planned future development includes:

* Branch site integration
* Site-to-site IPsec VPN
* Layer 2 security
* Additional redundancy scenarios
* Dynamic routing
* Additional security and troubleshooting scenarios

The goal is to progressively expand the lab while documenting the configuration, verification, failures, and lessons learned from each stage.
