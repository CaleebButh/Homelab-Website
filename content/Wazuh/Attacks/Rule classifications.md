See also:[[Brute force SSH]]

The rule levels in Wazuh communicate both importance and details of the alert. 
For example:

**Level 5 alerts**
- *User generated error*
- Missed passwords
- Denied actions
- No relevance in isolation

**Level 10 alerts**
- **Multiple user generated errors**
- Multiple password failures
- Multiple failed logins 
- Indicates an attack or somebody forgot credentials.

Source:  [Rules Classification: Wazuh Docs](https://documentation.wazuh.com/current/user-manual/ruleset/rules/rules-classification.html)

**Level 8 alerts** Typically are "First time seen events", but they can also be "security relevant actions such as the activation of a sniffer or similar activities." I would assume that exceeding auth attempts counts as a "security relevant action."
![[Pasted image 20260420183016.png]]