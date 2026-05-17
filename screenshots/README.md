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

# Connectivity Test

First the changes to the machine settings:

![VLAN Creation](Images/Win-Machine-1-IPV4-setup.png)
(PC 2 is set to 10.10.10.11)
Then a ping test. I set VLAN 10 to use both Port 6 and 1 to see if devices in the same VLAN can communicate with each other.

![VLAN Creation](Images/(1)-VLAN-Connectivity-Test.png)

From Machine 2 -> 1:

![VLAN Creation](Images/(1)VLAN-Connectivity-Test-(2).png)

Then I set device 2 into another VLAN (VLAN 30) to test if communication still works.
Device 2 is now connected to port 3 with an IP of 10.10.30.10, testing connectivity both ways.

Device 2 can ping its SVI (10.10.30.1) but not VLAN 10's (10.10.10.1) or Device 1 (10.10.10.10)

![VLAN Creation](Images/(2)-VLAN-Connectivity-Test.png)

Vice versa for Device 1.

![VLAN Creation](Images/(2)-VLAN-Connectivity-Test-(2).png)

# Attack Simulation

In a Kali Linux VM, the follow commands were run for the target system:
sudo ip addr flush dev eth0 (clears all old configs for interface)
sudo ip addr add 10.10.10.50/24 dev eth0 (Assigns IP to device to eth0)
sudo ip link set eth0 up (Turns interface eth0 on)
sudo ip route add default via 10.10.10.1 dev eth0 (establishes 10.10.10.1 as the gateway)

Then tested for connectivity to the gateway

![VLAN Creation](Images/VM-Connectivity-Test-(V10)).png)

Success.

Next, setting up the attacker system:

sudo ip addr flush dev eth0
sudo ip addr add 10.10.20.50/24 dev eth0
sudo ip link set eth0 up
sudo ip route add default via 10.10.20.1 dev eth0

Also a successful connection to the gateway.

![VLAN Creation](Images/VM-Connectivity-Test-(V20)).png)



