**Wazuh SIEM Setup**
To start out. My home lab consists of three VMs. A manager VM, which hosts my Wazuh-manager, an attacker machine (Kali Linux) and one Agent VM. The Wazuh agent and manager are both on Ubuntu 24.02.

I set them up according to the documentation found here: [Docs](https://documentation.wazuh.com/current/quickstart.html)

Manager IP: 192.168.40.135
Agent IP: 192.168.40.150
Attacker IP: 192.168.40.77

Both agent/manager VMs are properly configured with the agent forwarding logs to the manager.
![[Pasted image 20260420153422.png|582]]
Above is a screenshot of the dashboard showing one active agent.


By the end of this project I want  to have designed and operated a functional home SOC using Wazuh that can detect attacks, classify them and investigate them. 

Overall objectives:

1. build the environment
2. Generate real attack data.
3. Detect it with Wazuh
4. Investigate it as an analyst.
5. Improve detection over time.

See also: [[Attacks!]], [[Defending and Alerting]]