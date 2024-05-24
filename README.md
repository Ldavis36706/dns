<p align="center">
<img src="https://i.imgur.com/RtQ7SeN.png" alt="DNS"/>
</p>

<h1>Domain Name Service(DNS) Management and Troubleshooting </h1>
This tutorial outlines how to manage DNS records and understand DNS cache behavior.

.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Line Interface

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Overview Steps</h2>

Step 1 A-Record Exercise
  - Connect/log into Domain Controller virtual machine as your domain admin account (mydomain.com\jane_admin)
  - Connect/log into Client virtual machine as an admin (mydomain\jane_admin)
  - From Client virtual machine try to ping “mainframe” notice that it fails
  - Nslookup “mainframe” notice that it fails (no DNS record)
  - Create a DNS A-record on Domain Controller virtual machine for “mainframe” and have it point to Domain Controller virtual machine Private IP address
  - Go back to Client virtual machine and try to ping it. Observe that it works


Step 2 Local DNS Cache Exercise
  - Go back to Domain Controller virtual machine and change mainframe’s record address to 8.8.8.8
  - Go back to Client virtual machine and ping “mainframe” again. Observe that it still pings the old address
  - Observe the local dns cache. (ipconfig /displaydns)
  - Flush the DNS cache (ipconfig /flushdns). Observe that the cache is empty
  - Attempt to ping “mainframe” again. Observe the address of the new record is showing up



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

