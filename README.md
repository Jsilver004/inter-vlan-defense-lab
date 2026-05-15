# inter-vlan-defense-lab

This project demonstrates how VLAN segmentation, inter-VLAN routing controls, and ACL enforcement can reduce lateral movement inside an enterprise network.

This lab simulates an attacker attempting to move between VLANs and demonstrates how ACLs and secure switch configurations mitigate unauthorized communication.

# Objectives

- Configure VLAN segmentation on a Layer 3 Cisco switch
- Enable and test inter-VLAN routing
- Simulate lateral movement attacks
- Restrict unauthorized VLAN communication using ACLs
- Mitigate VLAN hopping risks
- Validate segmentation effectiveness through testing

## 1.Tools/Technologies

- Cisco Layer 3 Switch
- PuTTy
- Kali Linux VM
- Windows 11 Machine
- Oracle VirtualBox
- Hyper-V
- ACLs
- VLANs
- InterVLAN Routing

 ## Network Topology

 ## Lab Setup

 - Creation of VLANS 10(HR), 20(Finance), 30(IT), and 40(Sales) and assigning them ports (Gi/0/1-4)

### VLAN/Port Configurations

   | VLAN | Deptartment | Gateway | SVI Port |
   |---|---|---|---|
   | 10 | HR | 10.10.10.1 | Gi/0/1 |
   | 20 | Finance | 10.10.20.1 | Gi/0/2 |
   | 30 | IT | 10.10.30.1 | Gi/0/3 |
   | 40 | Sales | 10.10.40.1 | Gi/0/4 |


The following actions were performed during setup:
1.  Enabled Layer 3 routing by enabling "ip routing"
2.  Created VLANs on the switch through using "configure terminal" and creating VLANS (e.g. vlan 10)
3.  Configuring Switch Virtual Interfaces (SVIs) by using "interface vlan x"
4.  Assigned physical switch ports to access the VLANs
5.  Configured a trunk port for VLAN traffic across a single physical port
6.  Accessing the ports via "switchport mode access" and "switchport vlan x" to assign ports to VLANS

### Host Configurations

Two Windows hosts were configured with static IPs for connectivity tests.

Configurations:

   | Device | VLAN | IP address | 
   |---|---|---|---|
   | PC 1 | VLAN 10 | 10.10.10.10 | 
   | PC 2 | VLAN 10 | 10.10.10.11 |

and:
   | Device | VLAN | IP address | 
   |---|---|---|---|
   | PC 1 | VLAN 10 | 10.10.10.10 | 
   | PC 2 | VLAN 39 | 10.10.30.1 |

Testing demonstrated:
- Devices could successfully ping their own VLAN Gateways
- Devices in separate VLANs could NOT communicate after ACL enforcement

Detailed switch configurations and ACL rules are located in /config.

### Attack (IP)

## 7. VLAN Hopping Protection

In addition to restricting inter-VLAN comminucation through ACL enforcement, the lab also addresses VLAN hopping risks caused by inseucre switch port configurations.

### VLAN Hopping Risks

Switch ports that are configured using dynamic trunking mode can negiotate trunk connects through Dynamic Trunking Protocol (DTP). This introduces a security risk, as an attacker may attempt to form an unahtorized trunk connection to gain access to other VLANs.

A misconfigured switch port may allow:
- Unauthorized VLAN access
- Traffic sniffing across VLANs
- Lateral movement between departments
- Expansion of attack surfaces

### Insecure Configuration

To mitigate this risk, the following protections were implemented:
- Disabled Dynamic Trunking Protocol (DTP)
- Force the port into access mode
- Restrict the port to a single VLAN
- Prevent unauthorized trunk negiotation

Example:
 switchport mode access
 switchport access vlan 10
 switchport non-negotiate

Security Impact: By forcing the port into static access mode and disabling DTP negiotation, unauthorized trunk formation was prevented: This mitigates the chances of VLAN hopping attacks and strengthens network segmentation by ensuring devices can only access their assigned VLAN.

Validation: Testing confirmed unauthorized VLAN access through trunk negotiation was no longer possible after secure port configurations were applied.
