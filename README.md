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

# Tools/Technologies

- Cisco Layer 3 Switch
- PuTTy
- Kali Linux VM
- Windows 11 Machine
- Oracle VirtualBox
- Hyper-V
- ACLs
- VLANs
- InterVLAN Routing

 # Network Topology

 # Lab Setup

 - Creation of VLANS 10(HR), 20(Finance), 30(IT), and 40(Sales) and assigning them ports (Gi/0/1-4)
   | VLAN | Deptartment | Gateway |
   |---|---|---|
   | 10 | HR | 10.10.10.1 |
   | 20 | Finance | 10.10.20.1 |
   | 30 | IT | 10.10.30.1 |
   | 40 | Sales | 10.10.40.1 |
