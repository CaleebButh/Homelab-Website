See also: [[Table of contents]]

With the firewall configured and the initial network topology established, the next step was deploying an Active Directory environment. To guide the setup process, I followed the official Proxmox Windows Server best practices documentation, available [here](https://pve.proxmox.com/wiki/Windows_2022_guest_best_practices).

OS tab:

1. Select ISO image
2. Type: Microsoft windows
3. Version: 11/2022/2025

System tab:

1. Machine set to q35 (this enables PCIE passthrough)
2. SCSI controller: VirtIO SCSI single
3. BIOS: OVMF (UEFI)
![[Pasted image 20260525195251.png]]

Disks tab:

1. Bus/Device set to SCSI
2. Disk size set to 70GB
3. Cache set to write back and discard is ticked
4. IO thread enabled
![[Pasted image 20260525195629.png]]

CPU/Memory

Set cores to 2 and ram to 4GB for now.
![[Pasted image 20260525195807.png]]
![[Pasted image 20260525195820.png]]

Network:

1. set network bride to vmbr10
2. Model set to VirIO
![[Pasted image 20260525200010.png]]

Final touch:

While reviewing the Proxmox best practices documentation, I found that additional VirtIO drivers are required for optimal compatibility and performance when running Windows guests under Proxmox.

To address this, I downloaded the VirtIO driver ISO and attached it as an additional CD/DVD drive to the VM.

![[Pasted image 20260525200840.png]]

<h1>Final setup in VM</h1>
Selected Windows Server 2022 Standard Evaluation (Desktop Experience)
![[Pasted image 20260525201340.png]]

Clicked on Load driver to load the virtIO drivers
![[Pasted image 20260525201443.png]]

Installed drivers from all three locations listed in Guidelines.
![[Pasted image 20260525201533.png]]![[Pasted image 20260525201609.png]]
![[Pasted image 20260525201706.png]]

Finally, I installed the OS on my 70GB partition.
![[Pasted image 20260525201723.png]]



<h1>Post install configuration</h1>
With the operating system up and running there are just a few things left to do. 


<h2>QEMU guest agent installation</h2>
The mouse pointer was off, in order to fix this, I installed the QEMU guest agent via the installer at D:\guest-agent
![[Pasted image 20260525202705.png]]

<h2>Additional VirtIO drivers and services</h2>
Resource usage reporting inside Proxmox appeared inaccurate, with CPU and memory usage showing abnormally high values. This was resolved by installing the remaining VirtIO drivers and services included on the driver ISO.

![[Pasted image 20260525202830.png]]

With these components installed, the Windows Server VM now has:

- proper VirtIO networking support
- improved storage performance
- accurate resource reporting
- better Proxmox integration

At this point, the Windows Server 2022 VM is fully operational and ready to be promoted into an Active Directory domain controller.