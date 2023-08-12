<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users

<h2>Deployment and Configuration Steps</h2>
<br />
<br />
Create the Domain Controller VM (Windows Server 2022) and set the NIC Private IP address to static. Then create a client virtual machine with the same vnet and resource group as the Domain Controller VM.
<br />
<br />
<img src="https://i.imgur.com/9RdXafC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Login to Client VM with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping). if it fails, login to the Domain Controller and enable ICMPv4 in on the local windows Firewall. Then finally go back to Client VM to see that it has succeeded 
<br />
<br />
<img src="https://i.imgur.com/npQuV1E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Go to DC-1 server's manager, and click add roles and features. Then complete the installation process by simpling clck next and checking the active directory box and eventually install. After it is done installing, click on the flag at the top right corner, clcik promote the server, add forest, type your domain name and finish installation. DC-1 should restart after it has been installed. 
<br />
<br />
<img src="https://i.imgur.com/0UAb02v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Login to Active Directory again, go to Active Directory Users and Computers, create an Organizational Unit called “_EMPLOYEES”. Create another OU and name it _ADMIN. Now right click on _ADMINS, sroll to add and then user. Fill in all the necessary boxes and click add. Now the user is in a folder that says admin but the user is not yet an amdin. To do that, Right click the user account -> click properties -> member off -> add -> type admin and then click ok. 
<br />
<br />
<img src="https://i.imgur.com/al4Glwo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Go to Azure portal and set Client VM DNS settings to the DC’s Private IP address. Then restart Client VM to update the changes. Now we are going to try and add Client to the DC.
Right click start and click system -> Click on Add PC Advanced  -> Click on change,domain  -> Type domain name -> Then click ok and t should restart after. After it restarts, Login to the Domain Controller VM and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain.
<br />
<br />
<img src="https://i.imgur.com/KfZrsyH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Log into Client VM as an admin user and open system properties, click “Remote Desktop”, and allow “domain users” access to remote desktop.
You can now log into Client VM as a normal, non-administrative user. 
<br />
<br />
<img src="https://i.imgur.com/Tu2XhWY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
