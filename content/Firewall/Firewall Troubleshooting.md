While setting up active directory, I realized I was unable to reach the web from my windows server, meaning my firewall was not forwarding any traffic to my network yet. (this makes sense because I have not done any configuration on the firewalls end.)

I started by making sure I could ping my firewall from my windows server vm
![[Pasted image 20260528200719.png]]

I then tested pinging my home router, on the other side of the firewall.
![[Pasted image 20260528200943.png]]
Destination host unreachable. My firewall is halting anything from getting in or out. Very secure indeed but not what I, or anybody else wants from a good firewall. Lets do some configuring. 

Logging in to the firewalls web interface I can see the rules for WAN/LAN. I am thinking I found the culprit in the WAN rules. 

![[Pasted image 20260528201429.png]]

This rule looks like it blocks all traffic from private networks. Most likely not a big deal when your firewall is connected to the internet but mine is not, it is connected to my home network which is connected to the internet. 

After some digging I found a setting that could also be contributing under interfaces > WAN.
![[Pasted image 20260528201632.png]]
I unchecked this box. We will save these changes and see if we can ping out now. I will do some firewall hardening/rule writing at a later date.

This worked! I can now ping out to 1.1.1.1 from my windows VM.

back to [[Setting up active directory]]