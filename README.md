<h1 style="color:blue;"> SIEM Configuration with Azure</h1>


<h3 Resources Used </h3>
<ul type="circle">
 <li>Microsoft Azure</li>
 <li>Windows Power Shell</li>
</ul>


<h3>Overview</h3>
The lab consists of creating a home SOC using Microsoft Azure. 

<br>A virtual machine acts as the honeypot to attract potential attackers to attempt failed login attempts. These failed attack attempts are logged in a central repository that will be configured to an SIEM (Microsoft Sentinel) and queried to create an attack map.

<h3>Initial Set up</h3>

First, a resource group within Microsoft Azure is created to host cloud resources for the project. Then a virtual machine named <b> Honeypot VM </b> is made within a virtual network which will be used as a target for potential attackers. 

<br> Both the network security group or cloud firewall and the default Windows firewalls within the virtual machine are turned off to heighten the vulnerability of the machine.

<br> <img src="Images/Screenshot 2025-02-13 152426.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> <img src="Images/Screenshot 2025-02-13 152556.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>
