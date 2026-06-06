See also: [[Table of contents]]

Now it's time to create some OUs to organize our domain. 

In active directory users and computers we will right click on the domain and select new, Organizational Unit:
![[Pasted image 20260606141747.png|458]]

I created an OU names "Diodes" to reflect my company name. Within this OU I created several more to further organize things.
![[Pasted image 20260606142348.png]]


<h1>Creating Users</h1>
Under the Users OU, we can now create a test user
![[Pasted image 20260606143605.png]]

Under the "admins" OU
![[Pasted image 20260606143757.png]]
This account gets added to the "Domain Admins" security group.
![[Pasted image 20260606151525.png]]

Now we have OUs created and multiple user accounts. One regular domain user and one admin account. Time to set up a workstation and join it to the domain.

[[Joining a windows machine to the domain]]