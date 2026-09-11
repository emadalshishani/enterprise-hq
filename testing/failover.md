# HQ SVI Failure and Recovery Test

## 1. Test Objective

The objective of this test is to verify the impact of an SVI failure on endpoint connectivity and confirm service recovery after the SVI is restored.

This test uses VLAN 30 and PC-HQ-01.

## 2. Test Environment

| Component       | Configuration   |
| --------------- | --------------- |
| PC              | PC-HQ-01        |
| VLAN            | 30              |
| PC IP           | 192.168.30.2/29 |
| Default Gateway | 192.168.30.1    |
| L3 SVI          | Vlan30          |
| L3 SVI IP       | 192.168.30.1/29 |

## 3. Failure Test

The VLAN 30 SVI was administratively disabled on the L3 switch:

```text
interface vlan 30
shutdown
```

The switch reported:

```text
Interface Vlan30, changed state to administratively down
Interface Vlan30, changed state to down
```

A connectivity test was then performed from PC-HQ-01 toward the SRX:

```text
ping 10.10.10.1
```

Result:

```text
host (192.168.30.1) not reachable
```

### Result

**PASS**

The failure was observed as expected because the default gateway `192.168.30.1` was unavailable.

## 4. Recovery Test

The VLAN 30 SVI was restored:

```text
interface vlan 30
no shutdown
```

The switch reported:

```text
Interface Vlan30, changed state to up
Interface Vlan30, changed state to up
```

PC-HQ-01 was then tested again:

```text
ping 10.10.10.1
```

The first ICMP request timed out while the interface was recovering, followed by successful replies.

### Result

**PASS**

Connectivity was restored after the SVI returned to the up/up state.

## 5. Conclusion

The test confirms that:

1. VLAN 30 connectivity depends on the availability of its L3 SVI.
2. Disabling the SVI causes the VLAN 30 default gateway to become unavailable.
3. Restoring the SVI restores connectivity.
4. The current topology does not provide gateway redundancy.

This is an SVI failure/recovery test and **not an HA or VRRP failover test**.

Actual gateway redundancy will be tested in a future phase after VRRP is introduced.
