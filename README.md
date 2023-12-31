# Active directory

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines. <br />


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

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/0639dc40-1330-4281-87cf-00297387bf77)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/b611f634-b89f-4828-a4ee-1b19bf94a732)



in our Client Virtual Machine, go to 'Start' and click 'System', then 'Rename this PC (advanced)', then click 'Change' under Computer Name, then go down to 'Member of' and click 'Domain'. In the box below, type in the name we set for the server before. Next, you will be prompted by Windows Security to enter the name and password in order to join the domain, so put the name of the server and the username created previously, seperated by a forward slash (ex. mydomain.com\jane_admin), and use the password that was set for the admin account previously

Following this step, we will set up remote desktop for the non-administrative users on the Client VM 

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/e45f3bd2-d9fa-4744-a714-7ed8362b1b4b)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/036e21e1-bdd6-4438-bf0b-4e97f063178f)


After logging in to our Client VM, go to the 'Start' menu and click 'System', then on the right side of the window click 'Remote Desktop', then click 'Select Users that can remotely access this PC' 

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/b132b947-407d-42ab-893a-1ffa59628154)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/4af569ea-9447-4e21-8fe6-0d3374f0f567)


This window shows who is able to remote desktop into this PC, so in order to make it so all guest users can remote into the Domain Server, we can add the entire group called 'Domain Users' so any user in that group will have the ability to remote in to the PC.
To do this, click 'Add' and then write in 'Domain Users' in the box at the bottom and click 'Check Names', then 'OK' 

Finally, we will use a script to create many users and attempt to log in to our Domain Server with one of our new users to make sure we have set up everything properly

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/a1e2c92e-147c-4e91-a2c5-140566da1f59)

After logging into our Domain Client VM as our 'jane_doe' admin account, we will go to 'Start' and open up Windows Powershell

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/f7516a75-ff63-4561-b795-59ecb4e381ad)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/c5d9c31d-fa4e-4f09-a73c-84059c732e5a)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/b0bade80-41bf-4cbc-a810-aa9638268d49)


Next, copy the script that creates all the new users and Paste it into Powershell as a 'New Script' on the top left of the window and click 'Run Script', this will begin creating many users over a period of time. 

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/bd3d1fb2-5b7d-49bc-976d-719557558d8c)

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/ebf94780-c90c-4f81-92ba-e1d0f5a634ad)


Then, go back into Active Directory under the '_EMPLOYEES' Organizational Unit, and there should be all the user accounts created by the script. To ensure the accounts were created and can be used successfully, choose any of the users and log in to the Domain Controller VM with that users credentials, the password will be 'Password1' because that is that password for all the user accounts created with the script

![image](https://github.com/chrisfortuno/Activedirectory/assets/149267076/2ffe2734-f9bf-4832-ad62-35319f5bf2fc)

If successful, you should be greeted with the login welcome screen. Once these user accounts are created and sorted into the '_EMPLOYEES' group, you can now easily give out these accounts to individual users, give or take away privileges or access to specific files or folders, reset passwords and much more using Active Directory 




















