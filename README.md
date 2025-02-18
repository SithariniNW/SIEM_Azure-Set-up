<h1 style="color:blue;"> SIEM Configuration with Azure</h1>


<h3 Resources Used </h3>
<ul type="circle">
 <li>Microsoft Azure</li>
</ul>


<h3>Overview</h3>
The lab consists of creating a home SOC using Microsoft Azure. 

<br>A virtual machine acts as the honeypot to attract potential attackers to attempt failed login attempts. These failed attack attempts are logged in a central repository that will be configured to an SIEM (Microsoft Sentinel) and queried to create an attack map.

<h3>Initial Set up</h3>

First, a resource group within Microsoft Azure is created to host cloud resources for the project. Then a virtual machine named <b> Honeypot VM </b> is made within a virtual network which will be used as a target for potential attackers. 

<br> Both the network security group or cloud firewall and the default Windows firewalls within the virtual machine are turned off to heighten the vulnerability of the machine.

<br> <img src="Images/Screenshot 2025-02-13 152426.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> <img src="Images/Screenshot 2025-02-13 152556.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> <img src="Images/Screenshot 2025-02-16 225508.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

After the creation of the initial architecture, I tried connecting to the created virtual machine through Windows Remote Desktop Connection. However, it was unsuccessful since the VM did not allow RDP connections. Therefore an inbound rule had to be configured to allow RDP connections and remotely connect to the VM.

<br> <img src="Images/Screenshot 2025-02-13 221617.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> <img src="Images/Screenshot 2025-02-13 220114.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> Then within the VM, Windows Firewall settings were completely turned off, to ensure that the machine was completely vulnerable. This can be tested by sending a ping request to the VM through the host machine. Which became successful since it is open to making connections.

<br> <img src="Images/Screenshot 2025-02-16 153308.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3>Log Repository Creation</h3>

For the use of our log repository, a Log Analytics Workspace is created within Microsoft Azure.

<br> <img src="Images/Screenshot 2025-02-13 154136.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

To analyze the collected log data further using an SIEM, a  Microsoft Sentinel instance is also created and connected to the log analytics workspace. 

<br> <img src="Images/Screenshot 2025-02-13 213622.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> Furthermore, a connection between the VM and log analytics workspace should also be created. This is done through several steps,
<ul>
 <li> Installing Windows Security Events in Sentinel</li>
 <li> Installing Windows Security Events via AMA package </li>
 <li> Configure data connection rule (allows VM to forward security logs to log analytics workspaces) </li>
</ul>

<br> <img src="Images/Screenshot 2025-02-17 170046.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> After the above steps are completed, the logs at the created Log Analytics Workspaces will be able to display logs regarding any activities taking place within the VM.

<br> <img src="Images/Screenshot 2025-02-17 220447.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3> Querting log repository using KQL</h3>

KQL or Kusto Query Language is a tool in Microsoft Azure similar to SQL that can be used to explore and filter data.

<br> KQL can be used to filter through the many security events that occur within the VM to narrow down specific events. As an example to analyze results that indicate a failed login attempt the following query can be used,

<br> <img src="Images/Screenshot 2025-02-18 213548.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3> Uploading data to SIEM </h3>

Using a table of geographical locations of IP address ranges combined with the security event logs of the VM, a mapping of the locations of the attacks can be created through the Microsoft Sentinel SIEM.

<br> <img src="Images/Screenshot 2025-02-17 230830.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3> Conclusion </h3>

This project successfully demonstrated how to configure a Security Information and Event Management (SIEM) system using Microsoft Sentinel within Azure. By creating a honeypot VM, disabling security measures, and logging failed login attempts, we were able to collect valuable security data and analyze it using Kusto Query Language (KQL). The integration of Microsoft Sentinel allowed us to visualize attack patterns and understand potential threats targeting the system.

<h3> Reflection </h3>

One of the key takeaways from this project was the importance of proactive monitoring and logging in cybersecurity. It also gave me a glimpse of the workings of real-world SIEM and SOC. This lab served me as a foundational exercise for building more advanced security monitoring solutions.

<h5> Skills obtained </h5>

<ul> 
 <li> Microsoft Azure configurations </li>
 <li> Kusto Qurey Language </li>
 <li> Working with SOC and SIEM setup </li>
</ul>

<h5> References </h5>
https://www.youtube.com/watch?v=g5JL2RIbThM
<br> https://www.youtube.com/watch?v=RoZeVbbZ0o0&t=1580s
<br> https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-transformations
<br> https://learn.microsoft.com/en-us/azure/azure-monitor/logs/custom-fields
