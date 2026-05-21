# 2. Layer 2 Reconaissance

## Objective
Analyze how inproper use of protocols can be observed by an attacker through packet captures and used to conive avenues to break into a network and compromise it's systems.

## Set up

A Kali linux VM was configured with the following:

![VLAN Creation](../screenshots/Images/Attacker-Setup.png)

It the L3 switch was set up with the insecure Dynamic Trunking Protocol (DTP) and CDP (Cisco Discovery Protocol)

![VLAN Creation](../screenshots/Images/DTP-Enable.png)
![VLAN Creation](../screenshots/Images/EnableCDPpng.png)

