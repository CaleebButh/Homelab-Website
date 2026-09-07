
// SSH 

***ssh-keygen -t ed25519***

Copies A public key to a remote computer (Assumes .ssh directory is set up)
***Get-Content (Path to PUBLIC key) | ssh username@remote IP "cat >> ~/.ssh/authorized_keys"***

No .ssh setup: 
***Get-Content C:\Users\caleb.admin\.ssh\id_ed25519.pub | ssh caleb@192.168.10.20 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys"***

configs for ssh are stored at ***/etc/ssh/sshd_config.d/***
This config may require temporary editing to allow a file to be copied from a new computer.

//