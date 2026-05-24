See also [[Defending and Alerting]]

Wazuh has command monitoring capabilities, this means it can detect specific commands when ran on a specific endpoint. Allowing us to monitor specific command usage. 

![[Pasted image 20260422194219.png]]
By adding the above  xml to the configuration file at /var/ossec/etc/ossec.conf, We can periodically get a list of running processes. (Every 30 seconds) on the *agent*.

![[Pasted image 20260422194330.png]]
By adding these lines to the config file at /var/ossec/etc/rules/local_rules.xml, on the *Server*
We can take the output of processes gathered and check for matches, in this case we are checking for nc -l, which would mean netcat is listening for incoming connections on the endpoint.

![[Pasted image 20260426130522.png]]
Here we can see that wazuh created an alert using the custom rule to detect unauthorized process creation! 

See next: [[File Integrity Monitoring]]

[docs](https://documentation.wazuh.com/current/proof-of-concept-guide/detect-unauthorized-processes-netcat.html)