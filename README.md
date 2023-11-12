# Activedirectory

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

- Creating two virtual machines inside of Azure, one Domain Controller which acts as our server that runs Active Directory, and one client computer which can access the network
- Joining the Client PC to the Domain server
- Creating many user accounts on the domain server using a script

<h2>Deployment and Configuration Steps</h2>


![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/a164bea5-6655-458e-b355-d4a37959a707)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/8c0d1c47-3eab-4770-8335-486488a04336)

</p>
<p>
Creating our Domain Controller inside of Azure and setting its NIC private IP address to be Static rather than Dynamic 
</p>
<br />




![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/6019eb32-9b40-4b1b-9dc4-dd1678853992)

</p>
<p>
Create our Client Virtual Machine 
</p>
<br />



