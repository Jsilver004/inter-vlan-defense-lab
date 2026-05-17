## VLAN Creation

The following screenshot shows the VLAN configuration on the Layer 3 switch aftering entering:
  
enable
configure terminal

![VLAN Creation](Images/VLAN-Creation.png)

VLAN overview:

![VLAN Creation](Images/VLAN-Overview.png)

Then the SVIs must be created and configured to prevent outside traffic.

![VLAN Creation](Images/SVI-Config.png)
![VLAN Creation](Images/SVI-Config-(2).png)
![VLAN Creation](Images/SVI-Config-(3).png)

An overview of all the interfaces:

![VLAN Creation](Images/Interface-Overview.png)

# Attack Simulation 

First the changes to the attacker machine settings:

![VLAN Creation](Images/Win-Machine-1-IPV4-setup.png)

Then a ping test. I set VLAN 10 to use both Port 6 and 1 to see if devices in the same VLAN can communicate with each other.

(Images/Win-Machine-1-IPV4-setup.png)

