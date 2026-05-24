See also: [[Attacks!]]

To test detection capabilities in Wazuh, I simulated an SSH brute force attack from my Kali Linux box against a Wazuh-agent target. The goal was to observe how Wazuh handles individual authentication failures versus correlated brute force behavior.

From the Kali VM, I used Hydra to perform repeated SSH login attempts against the target system:
![[Pasted image 20260420182058.png|697]]
The attack targeted a non-existent username and used a password word list to generate continuous authentication failures.

***Initial detection***
At the start of the attack, Wazuh generated multiple Level 5 alerts, each corresponding to a single  failed ssh login attempts until hitting 8 total attempts. 
![[Pasted image 20260420184411.png]]
8 Attempts triggered a correlation-Based detection. Wazuh escalated the detection to a higher-level alert. 
![[Pasted image 20260420184655.png]]

***Interpretation***
This alert represents "Behavioral detection" Where many low level events correlate into a single attack pattern (Brute force attempt)

See next: [[Denial of service (DOS)]]

See also: [[Rule classifications]]
