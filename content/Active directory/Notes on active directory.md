See also: [[Table of contents]]

Active directory is a directory service that stores, lists and organizes information about elements in a Microsoft environment. This includes devices, users, and applications. 

It stores information on users in the form of usernames, real names, phone numbers, ect. It also provides an authentication and authorization system to network resources. For example, in our environment at work, AD checks a user logging in to the domain. We also add security groups to each account that allow access to certain internal resources. Any other resources are denied unless the user is explicitly given access to these resources via groups.

Active directory domains are organized logically into forests, domains, and trees. 
Currently, I only have one domain, so my forest, tree and domain all share the same name. 

Forest: corp.diodes.com
Tree:   corp.diodes.com
Domain: corp.diodes.com
DC:     DC01

<h1>Definition of terms</h1>
<h3>Forest</h3>
A forest is the entire AD security boundary. It is the highest level container. 

<h3>Tree</h3>
This is a group of one or more domains that share a contiguous DNS namespace. In my case, my only tree is corp.diodes.com. 

<h3>Domain</h3>
This is where users, computers, groups, policies and authentication live. This is what my windows machines will join. 


<h1>Diagram</h1>
![[AD Forest.png]]


See also: [[Creating the lab structure]]