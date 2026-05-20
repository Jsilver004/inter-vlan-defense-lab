# Attack Simulation

# 1. Inter-VLAN insecurity

## Objective

The purpose of this attack was to see if systems located in separate VLANs could communication freely across the network and to evaluate the segmentation controls properly restrict lateral movement

The simulated modeled a scenario in which an attacker compromises a host in one department and tries to access systems located in another VLAN.

---

## Setup

Two Kali Linux VMs were configured to simulate attacker and target systems inside different VLANs.

| Device | VLAN | IP Address |
| --- | --- | --- |
| Attacker VM | VLAN 10 | 10.10.10.50 |
| Target VM | VLAN 20 | 10.10.20.50 |

The following commands were used to configure the attacker system:

sudo ip addr flush dev eth0 (Removes all IPs associated with Eth0)
sudo ip addr add 10.10.10.50/24 dev eth0 (Sets the device to 10.10.10.50, belonging to 10.10.10.0/24)
sudo ip link set eth0 up (Activates interface)
sudo ip route add default via 10.10.10.1 dev eth0 (Sets 10.10.10.1 as the default gateway)

Target VM was configured similarly, but using VLAN 20 as the subnet and gateway (10.10.20.1)

## Initial Attack Test

Attack system in VLAN 10 attempted to communicate with the target system in VLAN 20

  ping 10.10.20.50

## Result

Successful ping.

This demonstrated that unrestricted inter-VLAN routing allowed direct communication between separate network segments.

Because no ACL restriction had been applied yet, the L3 switch routed traffic freely between VLANs.

## Security Risk

This behavior represents a major security weakness in an enterprise environment

If an attacker compromises a workstation inside one department, they may be able to:
- Access other departments
- Laterally move across the network
- undergo internal reconaissance
- run ransomware programs
Although VLANs logically separate broadcast domains, they do not automatically prevent routed communication between VLANs when L3 routing is enabled

## ACL Enforcement
To mitigate this risk, an ACL was configured and applied to VLAN 10.

The ACL denied communication from VLAN 10 to VLAN 20 while permitting other authorized traffic. 

  access-list 100 deny ip 10.10.10.0 0.0.0.255 10.10.20.0 0.0.0.255
  access-list 100 permit ip any any

Then applied to VLAN 10.

  interface vlan 10
  ip access-group 100 in

## Post-ACL Test
So when the ping request was sent again:

  ping 10.10.20.50

The ping failed.

The attacker could no longer communicate directly with VLAN 20 devices.

This confirms that ACL enforcement effectively restricted unauthorized inter-VLAN communication and reduced opportunities for lateral movement.

## Validation

| Test | Result |
| --- | --- |
| VLAN 10 -> Vlan 20 Pre-ACL | Successful |
| VLAN 10 -> Vlan 20 Post-ACL | Failed |
| VLAN Gateway Communication | Successful |
| Same-VLAN communication | Successful |

The results demonstrated that segmentation controls significantly improves network security while preserving legitimate VLAN functionality.

## Key Takeaways
This simulation reinforced several important network security concepts:
- Vlan segmentation alone is not sufficient without ACL enforcement
- Inter-VLAN routing should follow least-privilege principles
- ACLs help reduce lateral movement opportunities
- Internal network segmentation is critical for enterprise defense
- Security controls should be validated through testing as opposed to assumed security
  
# 2. Layer 2 Reconaissance

## Objective
Analyze how inproper use of protocols can be observed by an attacker through packet captures and used to conive avenues to break into a network and compromise it's systems.

## Set up

A Kali linux VM was configured with the following:


![VLAN Creation](./screenshots/Images/(2)-VLAN-Connectivity-Test.png)
![VLAN Creation](./screenshots/Images/Attacker-Setup.png)
