[[Table of contents]]

After not logging into this server for a long time, I realized I have a need. I need a password manager. my intention is to create an on premises password manager using a small Debian virtual machine to host it for my organization.

<h2>Reserving an ip for the server</h2>
After spinning up the new VM, I set up an ip reservation for the server using pfSense. 
 ***ip link show***: Displays all available network interfaces, this includes the devices MAC address.
In pfSense: Services > DHCP server 

![[Pasted image 20260903200943.png|700]]
Adding a new reservation at 192.168.10.20

After a reboot of my Debian VM, it is showing the IP address I reserved for it.

![[Pasted image 20260903201812.png]]

From my windows VM, I connected to the server VIA SSH. This required a user account password.
![[Pasted image 20260903211031.png]]

<h2>Setting up key authentication</h2>

Generated a new keypair: ***ssh-keygen -t ed25519***

Copied the public key to the Linux machine

1. Got the public key from my windows machine
2. Accessed the linux computer using ssh
3. Made the .ssh directory on the linux machine 
4. Copied the key into a new file titled "authorized_keys". 
5. Set the permissions for the .ssh directory, and for the file. 

**1.)** Get-Content C:\Users\caleb.admin\.ssh\id_ed25519.pub | **2.)** ssh caleb@192.168.10.20 **3.)** "mkdir -p ~/.ssh && **4.)** cat >> ~/.ssh/authorized_keys && **5.)** chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys"

I tested logging into ssh again with my windows VM. **Note the difference here, Its asking for a passphrase for my private key, rather than a user account password.**
![[Pasted image 20260903210817.png]]

<h2>Installing Docker</h2>
[Debian Docker install documentation](https://docs.docker.com/engine/install/debian/?utm_source=chatgpt.com#prerequisites)

The documentation gives a list of uneeded software packages. These can be uninstalled/checked for using the following command:

sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-doc docker-buildx podman-docker containerd runc | cut -f1)

![[Pasted image 20260905001032.png]]
None of these were present in my case. 

Setting up Docker's apt repo:
![[Pasted image 20260905001448.png]]

Installing the docker packages:

**sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin**

NOTE: I have added an entry in DNS to resolve vault.corp.diodes.com to the IP of the password server, 192.168.10.20

<h2>Setting up a reverse proxy and Vaultwarden</h2>
![[Pasted image 20260905134953.png]]
According to the documentation on github for Vaultwarden, the web vault requires the use of HTTPS and it is suggested to use a reverse proxy. I will be using Caddy for this. 

Caddy is a web server and reverse proxy. It will listen for inbound HTTPS connections on TCP 443, encrypt traffic between the client and server, and forward any requests to Vaultwarden. After Vaultwarden prepares a response, it returned to the client by Caddy. 

Caddy's configuration file will be fairly straightforward for now.

vault.corp.diodes.com {
    tls internal
    reverse_proxy vaultwarden:80
}

This tells Caddy:

Request:
https://vault.corp.diodes.com
          │
          ▼
       Caddy
          │
          ▼
http://vaultwarden:80

TLS internal  tells Caddy to issue the sites certification from its own internal CA. This will be trusted by our domain controller later. 

From our windows machine, we can see that DNS is properly resolving the fqdn and port 443 can be connected to. This is Caddy's port. Caddy takes the traffic, encrypts it, and forwards it to port 80, where vaultwarden lives.
![[Pasted image 20260905140218.png]]

Using my browser on my windows machine. I am able to access the password manager using its fqdn that I set up. 
https://vault.corp.diodes.com

Currently, the certificate is not trusted so we get some warnings when accessing it. Lets fix that.
![[Pasted image 20260905140654.png]]

<h2>Trusting the CA</h2>
NOTE: I generated a new key pair to use for ssh between my Domain controller and my password manager. 

To begin, I ran the command below. This copies the Caddy root Cert to my domain controller so I can import it and push it out via group policy.

scp caleb@192.168.10.20:/tmp/vault-caddy-root.crt .

I then navigated to group policy management > drilled down to corp.diodes.com > Right clicked Group policy objects > Selected New

![[Pasted image 20260905145233.png]]

Named it "Vault trusted Cert" and imported the certificate from the password server. 

I then linked this GPO to the organizations OU.
After a GPupdate on my windows workstation, I am no longer getting the "Not secure" message in my browser.

![[Pasted image 20260905145501.png]]

after installing the bit warden browser extension, logging in using the "Self hosted" option, I am able to save and use passwords in the browser! Mission accomplished.
![[Pasted image 20260905150623.png]]

Next, I decided I wanted something to monitor all of my core services so I can easily know when an issue has occurred and with what system. I decided to go with: [[Uptime Kuma]]