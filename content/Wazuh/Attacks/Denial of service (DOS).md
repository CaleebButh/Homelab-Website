In this scenario, I will be testing a denial of service style event. I want to see if I can properly detect it using Wazuh and explain what is happening. (Can I distinguish from "Normal")

1. **Spinning up a target service on the victim vm**

I decided to go with an apache web server. 

Sudo systemctl start apache2
![[Pasted image 20260421185659.png|697]]

2. Identify live services/open ports on the target machine using my attacker.

nmap -sV -O 192.168.40.150
![[Pasted image 20260421185850.png]]

From My attacker I have identified my target. The apache web server running on port 80. 



