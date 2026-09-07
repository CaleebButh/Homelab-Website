I figured a good place to start with furthering my security knowledge is the humble firewall. 

In pfSense:

**Changing Admin credentials**

Navigated to user manager in the firewall web GUI
![[Pasted image 20260902200337.png]]

And reset the admin password via the boxes highlighted. 
![[Pasted image 20260902200418.png]]

I wanted to have my own admin account as well, so I am not relying on a single, shared account.
![[Pasted image 20260902215900.png]]


**Denying access to the web gui**

By Default, PFsense denies any WAN traffice to its webGUI. I confirmed this by trying to reach in a web browser from my home network (outside our simulated network) 

**External**
![[Pasted image 20260902220738.png]]
![[Pasted image 20260902220846.png]]

**Internal**
![[Pasted image 20260902220910.png]]
![[Pasted image 20260902220936.png]]


