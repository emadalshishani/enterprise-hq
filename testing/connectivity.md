# HQ Connectivity Verification

## 1. Test Objective

The objective of this test is to verify connectivity between the HQ end devices, VLAN gateways, the Layer 3 switch, and the HQ SRX.

The test validates:

* VLAN gateway reachability
* Inter-VLAN routing
* L2-to-L3 trunk connectivity
* L3-to-SRX transit connectivity
* End-to-end connectivity across the HQ network

## 2. Addressing

| Device      |    VLAN | IP Address      | Gateway      |
| ----------- | ------: | --------------- | ------------ |
| PC-HQ-01    |      30 | 192.168.30.2/29 | 192.168.30.1 |
| PC-HQ-02    |      10 | 192.168.10.3/29 | 192.168.10.1 |
| PC-HQ-03    |      10 | 192.168.10.2/29 | 192.168.10.1 |
| PC-HQ-04    |      20 | 192.168.20.2/29 | 192.168.20.1 |
| SRX-HQ-01   | Transit | 10.10.10.1/30   | N/A          |
| L3-SW-HQ-01 | Transit | 10.10.10.2/30   | N/A          |

## 3. L3 Switch Verification

The L3 switch successfully reached:

| Destination  | Result |
| ------------ | ------ |
| 10.10.10.1   | PASS   |
| 192.168.10.2 | PASS   |
| 192.168.10.3 | PASS   |
| 192.168.20.2 | PASS   |
| 192.168.30.2 | PASS   |

All tested destinations returned 5/5 successful ICMP replies.

## 4. End-to-End Verification

### PC-HQ-01

PC-HQ-01 successfully reached:

| Destination  | Result |
| ------------ | ------ |
| 192.168.30.1 | PASS   |
| 192.168.10.3 | PASS   |
| 192.168.10.2 | PASS   |
| 192.168.20.2 | PASS   |
| 10.10.10.1   | PASS   |

This confirms inter-VLAN routing from VLAN 30 and connectivity toward the SRX.

### PC-HQ-02

PC-HQ-02 successfully reached:

| Destination  | Result |
| ------------ | ------ |
| 192.168.10.1 | PASS   |
| 192.168.30.2 | PASS   |
| 192.168.10.2 | PASS   |
| 192.168.20.2 | PASS   |
| 10.10.10.1   | PASS   |

This confirms VLAN 10 connectivity, inter-VLAN routing, and connectivity toward the SRX.

### PC-HQ-03

PC-HQ-03 successfully reached:

| Destination  | Result |
| ------------ | ------ |
| 192.168.10.1 | PASS   |
| 10.10.10.1   | PASS   |

### PC-HQ-04

PC-HQ-04 successfully reached:

| Destination  | Result |
| ------------ | ------ |
| 192.168.20.1 | PASS   |
| 10.10.10.1   | PASS   |

## 5. Verification Summary

The current HQ topology successfully provides:

* VLAN segmentation for VLANs 10, 20, and 30.
* Default gateway functionality on the L3 switch.
* Inter-VLAN routing between VLANs 10, 20, and 30.
* 802.1Q trunk connectivity between the L3 and L2 switches.
* Layer 3 connectivity between the L3 switch and the SRX.
* End-to-end connectivity from the HQ endpoints toward the SRX.

## 6. Conclusion

The current HQ baseline configuration is operational and passed the planned connectivity tests.

No configuration changes were required as a result of this verification phase.
