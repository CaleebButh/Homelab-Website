The first step to turn my new Windows server into a domain controller is to set a static IP. This can be done by going to the control panel > network and internet > change adapter settings. I selected my adapter and brought up the properties. 
![[Pasted image 20260527215437.png]]

From the properties page I double clicked on Internet protocol version 4 and set my static IP, subnet mask, default gateway, and DNS server IP here.

![[Pasted image 20260527215728.png]]

While working through this part of the process, I realized that web traffic was not properly forwarding through my firewall. Check out how I solved this here: [[Firewall Troubleshooting]]


Next, we need to rename the computer. In server manager, I went to local server > computer name and changed it here. This required a reboot.
![[Pasted image 20260528221757.png]]

Next, I went to "Add roles and features" and installed active directory roles:

![[Pasted image 20260528222122.png]]

Selecting installation type:
![[Pasted image 20260528222341.png]]

Select destination server:
![[Pasted image 20260528222415.png]]

Select server roles: 
![[Pasted image 20260528222643.png]]

Installation page:
![[Pasted image 20260528223151.png]]

Now it's time to promote it to a domain controller!
![[Pasted image 20260528223345.png]]

From here We will create a new forest:
![[Pasted image 20260528223545.png]]

Installation page: 
![[Pasted image 20260528223940.png]]

Following the reboot, I set the DNS server back to referring to itself. A domain controller should use itself for DNS.
![[Pasted image 20260528225318.png]]

now we have to configure the DNS forwarders.

Server manager > tools > DNS > select the DC > Forwarders >  Added two forwarders. This is so internal domain lookups stay on the DC while internet lookups go out to pfSense/cloudflare.
![[Pasted image 20260528225656.png]]

We can prove this works by running an nslookup on the domain name and on google.
![[Pasted image 20260528225838.png]]
The domain name resolves internally, while the website resolves externally.

This DC should be up and running! Next up is [[Creating the lab structure]]