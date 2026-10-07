[[Table of contents]]

Commands used: Sudo netplan status -a, 

Because I had already previously worked with Wazuh in my last version of my homelab, I decided I would go for it again and make good use of it. 

First, I spun up a new Ubuntu server, giving it plenty of Ram and disk space. I rolled a few new ssh keys and gave the server my public key, and locked down ssh. I edited the [netplan](https://ubuntu.com/server/docs/explanation/networking/configuring-networks/) configuration file to give it a static ip, created a new DNS entry pointing to the ip from wazuh.corp.diodes.com and am now ready to install Wazuh. I will be following the [installation documentation](https://documentation.wazuh.com/current/installation-guide/index.html)

![[Pasted image 20260921191541.png]]

I haven't gone into much detail here as I already have documented this process in more detail in: [[Wazuh]].

I have the dashboard up and running with two agents configured. One for my windows PC that I use for management and one for my linux server that hosts VaultWarden and Uptime Kuma.

I am tired of setting up new infrastructure. I really want to work on getting red team exercises off to the races. [[Building an attack range]]

