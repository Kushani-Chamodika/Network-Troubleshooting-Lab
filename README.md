# Network Troubleshooting Lab Using Cisco Packet Tracer

## Project Overview

This project demonstrates network configuration, troubleshooting, and connectivity verification using Cisco Packet Tracer. It focuses on identifying and resolving common network issues in a small enterprise network environment.

The network uses VLANs, router-on-a-stick inter-VLAN routing, and DHCP to provide IP configuration to end devices. Several faults were intentionally introduced, investigated, and resolved to develop practical network troubleshooting skills.

## Objectives

- Configure VLANs to separate network departments.
- Configure trunk links between a switch and a router.
- Implement inter-VLAN routing using router-on-a-stick.
- Configure DHCP for automatic IP address assignment.
- Identify and resolve common network connectivity issues.
- Verify network connectivity using troubleshooting commands.

## Technologies and Tools

- Cisco Packet Tracer 8.2.2
- Cisco IOS CLI
- VLAN Configuration
- IEEE 802.1Q Trunking
- Inter-VLAN Routing
- DHCP
- IPv4 Addressing and Subnetting
- ICMP Ping Testing

## Network Design

The network consists of:

- One Cisco 1941 Router
- One Cisco 2960 Switch
- Two PCs
- Two VLANs: ADMIN and IT

### VLAN and IP Addressing Plan

| VLAN | Department | Network | Default Gateway |
|---|---|---|---|
| VLAN 10 | ADMIN | 192.168.10.0/24 | 192.168.10.1 |
| VLAN 20 | IT | 192.168.20.0/24 | 192.168.20.1 |

### Switch Port Assignments

| Switch Port | Configuration |
|---|---|
| Fa0/1 | Access port - VLAN 10 (ADMIN) |
| Fa0/2 | Access port - VLAN 20 (IT) |
| Gi0/1 | 802.1Q trunk link to the router |

## Troubleshooting Cases

### Case 1: Incorrect VLAN Assignment

**Issue:** PC2 could not communicate with its default gateway.

**Root Cause:** Switch port `Fa0/2` was incorrectly assigned to VLAN 10 instead of VLAN 20.

**Troubleshooting Commands:**
- `show vlan brief`
- `ping 192.168.20.1`

**Solution:** Reassigned `Fa0/2` to VLAN 20.

**Verification:** Confirmed the correct VLAN assignment and restored successful communication with the default gateway.

### Case 2: Incorrect IP Address

**Issue:** PC2 could not communicate with its default gateway.

**Root Cause:** PC2 was configured with an IP address from the wrong subnet (`192.168.30.0/24`).

**Troubleshooting Command:**
- `ping 192.168.20.1`

**Solution:** Restored automatic IP configuration by selecting DHCP on PC2.

**Verification:** PC2 obtained a valid address in the `192.168.20.0/24` network and connectivity was restored.

### Case 3: Switch Port Shutdown

**Issue:** PC2 lost network connectivity.

**Root Cause:** Switch port `Fa0/2` was administratively disabled.

**Troubleshooting Command:**
- `show interfaces fastethernet 0/2 status`

**Solution:** Re-enabled the switch port using `no shutdown`.

**Verification:** Confirmed that the port was connected and PC2 could successfully reach its default gateway.

### Case 4: DHCP Configuration Problem

**Issue:** PC2 failed to obtain an IP address through DHCP and received an APIPA address (`169.254.12.49`).

**Root Cause:** The IT-DHCP pool contained an incorrect network configuration.

**Troubleshooting Commands:**
- `show running-config | section dhcp`
- `show ip dhcp binding`
- `show ip interface brief`

**Solution:** Corrected the IT-DHCP pool to use the `192.168.20.0/24` network with default gateway `192.168.20.1`.

**Verification:**
- PC2 successfully obtained IP address `192.168.20.11` through DHCP.
- Ping to the default gateway (`192.168.20.1`) succeeded with 0% packet loss.
- Ping from PC2 to PC1 (`192.168.10.11`) succeeded with 0% packet loss.

## Verification Commands

The following commands were used to verify the configuration and troubleshoot connectivity:

```text
show vlan brief
show interfaces trunk
show interfaces fastethernet 0/2 status
show ip interface brief
show running-config | section dhcp
show ip dhcp binding
ping 192.168.20.1
ping 192.168.10.11
```

## Screenshots and Evidence

Screenshots demonstrating the network topology, VLAN configuration, trunk configuration, DHCP bindings, and successful connectivity tests are included in the `screenshots` folder.

<!--
After uploading screenshots, add them like this:

![Network topology](screenshots/network-topology.png)
![DHCP binding](screenshots/dhcp-binding.png)
![Connectivity test](screenshots/connectivity-test.png)
-->

## Key Skills Demonstrated

- Network troubleshooting and fault isolation
- VLAN configuration and management
- Router-on-a-stick inter-VLAN routing
- DHCP configuration and verification
- IPv4 addressing and subnetting fundamentals
- Switch port management
- Network connectivity testing
- Cisco IOS CLI
- Technical documentation

## Project Files

- `Network-Troubleshooting-Lab.pkt` - Cisco Packet Tracer project file
- `screenshots/` - Network configuration and troubleshooting evidence

## Conclusion

This project provided practical experience in identifying, troubleshooting, and resolving common network configuration issues. It strengthened my understanding of VLANs, DHCP, inter-VLAN routing, IPv4 addressing, and connectivity verification in a simulated enterprise network.
