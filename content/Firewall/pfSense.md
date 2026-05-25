To begin building out the lab environment, I decided to start with the firewall infrastructure. Since the firewall acts as the primary entry point for traffic into the network, getting it configured properly is an important first step. I chose to use pfSense, a free and open-source firewall and routing platform widely used in homelab and enterprise environments alike.

While researching how to deploy pfSense within Proxmox VE, I found an excellent guide in the official Netgate documentation [here](https://docs.netgate.com/pfsense/en/latest/recipes/virtualize-proxmox-ve.html)

The documentation assumes a few prerequisites are already in place. Two of them were already handled during my Proxmox setup, but I did need to create an additional Linux bridge to act as the isolated LAN interface for the firewall VM. Since pfSense requires at least two network interfaces — one for WAN and one for LAN — I created a new bridge named vmbr10 to serve as the internal lab network.
![[Pasted image 20260525015537.png]]

Next, I created the pfSense virtual machine using the recommended settings from the documentation.

Under the OS tab:
1. Use CD/DVD disc image file (iso)
2. Storage: local
3. Guest OS type: Other
![[Pasted image 20260525011027.png]]

Under the system tab: 
1. Graphic card set to SPICE
![[Pasted image 20260525011144.png]]

Under the Hard Disk Tab:

1. Bus/Device set to VirtIO block
2. Disk size no less than 8gb. I set it to 10 to be safe.
![[Pasted image 20260525011828.png]]

Under the CPU tab:

1. Socket/cores both set to one
![[Pasted image 20260525011945.png]]


Under the memory tab:

1. At least 1024 MB
![[Pasted image 20260525012112.png]]

Under the network tab:

1. Set to vmbr0
2. Model: VirtIO 
![[Pasted image 20260525012431.png]]

Click add to create the VM. Now we have a firewall vm configured! We have a bit more to do on the VM itself. 

I followed the configuration instructions on the docs page linked above. 

1. Type n and press Enter to skip VLAN configuration
2. Enter vtnet0 for WAN
3. Enter vtnet1 for LAN
4. Press Enter if prompted for additional interfaces
5. Type y and press Enter to complete the interface assignment
![[Pasted image 20260525014300.png]]

By default, the LAN subnet was configured as 192.168.1.0/24. Since I wanted a cleaner and more intentional lab network structure, I changed the subnet to 192.168.10.0/24.

From the pfSense console menu, I selected:

2) Set interface(s) IP address

I then configured the DHCP range to:

Start: 192.168.10.100
End: 192.168.10.200

At this point, the firewall was fully operational and successfully serving as the gateway for the isolated lab environment.

now I have a working Firewall!