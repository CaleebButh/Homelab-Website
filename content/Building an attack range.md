I have decided to use Game of active directory for my attack range. 
https://github.com/Orange-Cyberdefense/GOAD

Goad is a pentest active directory lab project, It simulates a vulnerable active directory environment to practice attack techniques.

This is a diagram of what I will be setting up. It contains 5 VMs, 2 forests, and 3 domains
![[Pasted image 20260921195542.png|700]]

Because GOAD is an intentionally vulnerable environment. I would like to keep it seperated from the rest of my environment. 
I set firewall rules to isolate it from all my lab networks and other private networks. I gave it the ability to reach the internet (This will only be used for provisioning) and I explicitly deny any incoming traffic from the internet.
![[Pasted image 20260921200029.png]]

I spun up a new VM on prox. An ubuntu server for provisioning the rest of the lab. I followed the setup instructions to set up the provisioner.
![[Pasted image 20261003142111.png]]