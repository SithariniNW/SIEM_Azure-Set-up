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

<br> <img src="Images/Screenshot 2025-02-16 225508.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

After the creation of the initial architecture, I tried connecting to the created virtual machine through Windows Remote Desktop Connection. However, it was unsuccessful since the VM did not allow RDP connections. Therefore an inbound rule had to be configured to allow RDP connections and remotely connect to the VM.

<br> <img src="Images/Screenshot 2025-02-13 221617.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> <img src="Images/Screenshot 2025-02-13 220114.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> Then within the VM, Windows Firewall settings were completely turned off, to ensure that the machine was completely vulnerable. This can be tested by sending a ping request to the VM through the host machine. Which became successful since it is open to making connections.

<br> <img src="Images/Screenshot 2025-02-16 153308.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3>Log Repository Creation</h3>

For the use of our log repository, a Log Analytics Workspace is created within Microsoft Azure.

<br> <img src="Images/Screenshot 2025-02-13 154136.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

To analyze the collected log data further using a SIEM, a  Microsoft Sentinel instance is also created and connected to the log analytics workspace. Furthermore, a connection between the VM and log analytics workspace should also be created.


<br> <img src="Images/Screenshot 2025-02-13 213622.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>





