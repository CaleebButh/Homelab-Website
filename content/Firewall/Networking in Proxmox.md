See also: [[Table of contents]]

Out of the box, Proxmox VE creates a Linux bridge called vmbr0. This bridge functions like a virtual switch and is connected to the server’s primary physical network interface (nic0).

Because vmbr0 is directly connected to my home network, attaching a VM to it would effectively place that VM directly on the LAN. Since I wanted to create isolation for the homelab environment, I created a second Linux bridge named vmbr10.

Unlike vmbr0, vmbr10 is not attached to a physical network interface and exists entirely within Proxmox as an isolated internal network. To allow controlled communication between the external network and the internal lab environment, I deployed a pfSense firewall VM with two interfaces:

vtnet0 connected to vmbr0 (WAN)
vtnet1 connected to vmbr10 (LAN)

This places the firewall logically between the outside network and the internal lab network, allowing pfSense to control routing, NAT, DHCP, and traffic filtering between the two environments.

![[LabNet.jpeg]]

<h1>Bonds</h1>
A network bond in Proxmox combines multiple physical network interfaces (NICs) into a single logical interface. Think of it like bundling multiple Ethernet cables together so they behave as one connection.

They are commonly used for Redundancy and failover, load balancing, higher availability, and increased bandwidth. 

A Bond creates a virtual interface such as bond0, the bond is then attached to a linux bridge. VMs connect to this bridge, while the bridge sends traffic through the bonded interfaces. 
The mode I would most likely use would be active-backup. One NIC is active while the other waits as backup. This is extremely stable and redundant. 

<h1>VLANs</h1>

VLANs (Virtual Local Area Networks) allow a single physical network to be divided into multiple isolated logical networks. They are commonly used for segmentation, security, and organization, such as separating management devices, servers, lab environments, and guest networks. VLANs work by attaching a VLAN ID tag to Ethernet traffic, allowing switches and devices to determine which network the traffic belongs to. Devices in different VLANs cannot communicate directly unless a router or firewall performs inter-VLAN routing. VLANs are typically configured across multiple devices including managed switches, firewalls like pfSense, and hypervisors.

In Proxmox, VLANs are commonly implemented using a single VLAN-aware Linux bridge, such as vmbr0, connected to a managed switch through a trunk port carrying multiple VLANs. The bridge is configured with VLAN aware checked, 
![[Pasted image 20260525121122.png]]allowing VLAN-tagged traffic to pass through to virtual machines. Individual VMs can then be assigned VLAN tags directly in their network settings, placing them onto specific VLANs without requiring separate physical interfaces. The switch handles the VLAN tagging and isolation, while the firewall or router manages DHCP, firewall rules, and communication between VLANs.

