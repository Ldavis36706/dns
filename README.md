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

Step 1 Create a Domain Controller virtual machine (Windows Server 2022) 
  - Set Domain Controller’s NIC Private IP address to be static 

Step 2 Create the Client virtual machine (Windows 10).
  - Use the same Resource Group and Vnet that your Domain Controller is in.

Step 3 Ensure Connectivity between the client and Domain Controller
  - Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
  - Check back at Client-1 to see the ping succeed

Step 4 Install Active Directory
  - Login to Domain Controller virtual machine and install Active Directory Domain Services
  - Promote as a Domain Controller: Setup a new forest as mydomain.com (can be anything, just remember what it is)
  - Restart and then log back into Domain Controller virtual machine as user you just created: keshadomain.com\labuser(in my example)
 
  
Step 5 Create an Admin and Normal User Account in Active Directory
  - In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
  - Create a new OU named “_ADMINS”
  - Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
  - Add jane_admin to the “Domain Admins” Security Group
  - Log out/close the Remote Desktop connection to Domain Controller and log back in as “mydomain.com\jane_admin”
  - User jane_admin as your admin account from now on

 Step 6 Join Client-1 to your domain (mydomain.com)
  - From the Azure Portal, set Client-1’s DNS settings to the Domain Controller’s Private IP address
  - From the Azure Portal, restart Client-1
  - Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
  - Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain


 Step 7 Setup Remote Desktop for non-administrative users on Client-1
  - Log into Client-1 as mydomain.com\jane_admin and open system properties
  - Click “Remote Desktop”
  - Allow “domain users” access to remote desktop
  - You can now log into Client-1 as a normal, non-administrative user now


 Step 8 Create a bunch of additional users and attempt to log into client-1 with one of the users
  - Login to Domain Controller as jane_admin
  - Open PowerShell_ise as an administrator
  - Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
  - Run the script and observe the accounts being created
  - When finished, open ADUC and observe the accounts in the appropriate OU

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/actCv1S.png" height="80%" width="80%" alt="Static IP Address"/>
</p>
<p>
Setting the Domain Controller's IP Address to static ensures that it will not change once it's configured to the Client's DNS server.  
</p>
<br />

<p>
<img src="https://i.imgur.com/awG5qO5.png" height="80%" width="80%" alt="Configure Client's DNS Server to the Domain Controller"/>
</p>
<p>
Be sure that the Client's DNS Server is configured to the Domain Controller's static IP Address.
</p>
<br />

<p>
<img src="https://i.imgur.com/4Z5sH8D.png" height="80%" width="80%" alt="Install Active Directory"/>
</p>
<p>
Make sure you remember the forest domain you create. 
  
  
  <img src="https://i.imgur.com/FqyIgdo.png" height="80%" width="80%" alt="Domain User Permissions"/>
</p>
<p>
I allowed domain users access to remote desktop.
</p>

<img src="https://i.imgur.com/Jz7uKxX.png" height="80%" width="80%" alt="Powershell Script to Create Users"/>
</p>
<p>
It's very important that you use Powershell_ise as an administrator. By using the script I was able to automate the process of creating 10,000 users.
</p>

<img src="https://i.imgur.com/qUaM6FB.png" height="80%" width="80%" alt="Users Being Created"/>
</p>
<p>
These are some of the users being created.
</p>

<img src="https://i.imgur.com/ZQsOXSR.png" height="80%" width="80%" alt="Updating Permissions of Users"/>
</p>
<p>
I made changes to users permissions. I reset passwords, disabled accounts, etc. I then tested those permissions to ensure they worked. I had lots of fun building this lab.
</p>

