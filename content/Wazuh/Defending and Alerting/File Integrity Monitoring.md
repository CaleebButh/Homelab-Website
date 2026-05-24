See also: [[Defending and Alerting]]

Wazuh has a built in FIM monitoring module that can monitor for file system changes. It can detect the creation, modification, and deletion of files.
Wazuh also enriches the alert data by getting information about who/what process modified the data using who-data audit. 

We start on our wazuh Agent and add the following to the ossec.conf file. This points wazuh to a particular directory that I have created and tells it to report all changes in that directory.

```xml
<directories check_all="yes" report_changes="yes" realtime="yes">/Home/wazuha/FIM</directories>
```


After setting up FIM and pointing it to a directory, I created a text file in that directory. 
![[Pasted image 20260428174838.png|697]]
In the screenshot above we can see an alert created that says "file added to the system"

Drilling down into the alert it gives us the full path to the file and the file name as well!
![[Pasted image 20260428174948.png]]

After changing text in the txt file we get another alert
![[Pasted image 20260428175138.png]]
"Integrity checksum changed" Letting us know there were changes to the file

Finally, we can delete the file, which generates an alert as well. Very cool!
![[Pasted image 20260428175254.png|697]]

