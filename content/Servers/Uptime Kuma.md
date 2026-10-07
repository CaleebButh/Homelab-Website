(Hosted on Vault01)

[Installation instructions](https://github.com/louislam/uptime-kuma)

Uptime Kuma is a service health monitor. It will have a dashboard where I monitor different servers and services to see if they're working correctly.

Turns out, this is really easy to install and get up and running. 
I created a directory for it, a separate from my directory for vault warden. This keeps them seperate in case I need to restart either of them and not both.

sudo mkdir -p /opt/uptime-kuma
cd /opt/uptime-kuma

I created a compose file and added the following:

services:
  uptime-kuma:
    image: louislam/uptime-kuma:2
    container_name: uptime-kuma
    restart: unless-stopped
    ports:
      - "3001:3001"
    volumes:
      - ./data:/app/data

and I started the container

sudo docker compose pull
sudo docker compose up -d

After It was installed, I ran through the initial configuration by heading to:
http://192.168.10.20:3001

I added a new DNS entry and put it behind the reverse proxy. 

It can now be accessed via: ***status.corp.diodes.com***
![[Pasted image 20260905234854.png]]

Once I got it set up I made three monitors. Monitors are extremely easy to configure.

I set one for the main domain controller, one for the firewall and one for vaultwarden. 

Vaultwarden was initially not working properly because the Kuma server did not trust the certificate of the vaultwarden server. I fixed this by adding the root certificate as a read-only mount in the compose.yaml file for Kuma. 

Next, I decided to get back to the task at hand and get working on my security tooling. 
[[Wazuh v2]]





