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

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/3bfdfe5f-64b5-407d-88f2-ff254a437a59)

In our Domain Controller VM, go to 'add roles and features' in Server Manager so we can install Active Directory

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/50fc7695-1b26-459c-aa5c-6478cece4f67)

In the 'Server Roles' section, select 'Active Directery Domain Services' and contiunue clicking 'next', then 'install' at the end

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/31f44292-d75f-4e5d-a1a6-57c1a5b8afee)

Afterwards, go back to the Server Manager home page and click 'Promote this server to a domain controller' under the yellow triangle

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/b9036873-36cb-474e-a4ce-0c2882839dab)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/fe719cb4-641d-4726-9eb7-9b47fb3418a8)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/0285fba1-7cc6-4959-9e81-e3cda46f5834)


After clicking 'Promote this server to a domain controller', we will set a root domain name, and then a DSRM password, then continue to hit 'Next' then install

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/eeb6b7a6-4b0b-4c3c-b9c6-f96cc7025f3c)

After that, we will create an Admin account and a Normal User Account in Active Directory 

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/ef3ad27b-2e58-4348-866f-f72cdf7c85db)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/7842fd34-90c8-485c-bb7d-e342105c26a5)


In the directory, we'll create an Organizational Unit called '_EMPLOYEES' where we will put the the normal users in, and we will also create an Organizational Unit called '_ADMINS' for the Admin Users

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/0c516e17-88d0-4092-b6af-37fd0f96cc4a)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/21f846d0-00b9-459d-938c-783de0a22adf)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/63eee163-7ecd-439d-87d7-8330b56d951a)



In the Admins folder, we'll create a new User who will be the Admin of the server, we'll give them a generic username and password for now

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/e80a278b-13d0-4b9d-9672-b4534a650162)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/800e9a26-1831-4d22-a0df-670caa028b4c)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/c9a1a9eb-b09f-4597-95fc-6993c80a30b4)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/b259dacd-de9a-41ab-b2eb-263de4a49f3e)


Next, we need to give the user we just created Admin privileges by adding the user to the 'Domain Admins' security group. First we right click and go to 'Properties', 'Member of', then go down to 'add', type in 'Domain', then 'Check names', then Domain Admins and hit OK, then Apply

For our next step, we will be joining the Client Virtual Machine to the Domain server. First, we will need to set the Client VM's DNS settings to the Domain Controller VM's Private IP Address

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/a5985bbe-5e5e-49ed-bd9b-2b690e54d5f6)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/4a183721-9d27-48be-b8c4-1efd495d820b)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/8d9209b2-5c96-406a-81eb-27a687258d29)



Copy the Domain controller VM's NIC private IP address in Azure, then go to the Client VM, click on the 'Networking' tab and click on the name of the Network Interface. After that, go to the DNS servers tab and click 'Custom' under the DNS servers line. Where it says 'Add DNS Server', we will paste the NIC private IP Address we copied earlier into this box, then click save.


![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/c547f778-1cf8-45f8-9a89-f5ebe9d952c9)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/8f933003-6072-4429-ba4c-2d6c809186ec)


in our Client Virtual Machine, go to 'Start' and click 'System', then 'Rename this PC (advanced)', then click 'Change' under Computer Name, 


















