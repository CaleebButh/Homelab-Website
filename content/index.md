Recently, I was given an awesome gift. One that any self-study tech enthusiast would jump at the chance for. I was given a ProLiant dl360 Gen9 server! Retired from its original home, now moved into the cloud, It needed a new home. I decided I would take it and see what I could do with it. 

![[Pasted image 20260525001226.png]]

I have been working on a smaller scale home lab environment, which I have documented a bit in the folder [[Wazuh]], the acquisition of this server will allow me to make a truly special lab environment. 

I am currently building a large-scale homelab environment designed to simulate a modern enterprise network and security infrastructure. The lab will begin with the deployment of a pfSense firewall to serve as the core network gateway and segmentation point. From there, I will implement a Windows Active Directory domain controller along with multiple Windows workstations joined to the domain to emulate a realistic corporate environment.

Following the core infrastructure deployment, I plan to expand the lab’s defensive capabilities by integrating Wazuh and Security Onion for centralized logging, endpoint monitoring, intrusion detection, and network visibility. I will also deploy intentionally vulnerable targets to support penetration testing and attack simulation exercises. Finally, I will implement VLAN segmentation to isolate systems by function and improve network security architecture.

Planned VLAN structure:

VLAN	Purpose
10	Management
20	Servers
30	Workstations
40	Attacker
50	DMZ
60	Security Tools

This environment will serve as a platform for developing hands-on experience in systems administration, offensive security, defensive monitoring, network segmentation, and enterprise security operations. I will be documenting the entire process, configurations, and lessons learned throughout the project.

See Next: [[Table of contents]]
