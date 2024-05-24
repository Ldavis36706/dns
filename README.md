<p align="center">
<img src="https://i.imgur.com/RtQ7SeN.png" alt="DNS"/>
</p>

<h1>Domain Name System(DNS) Management and Troubleshooting </h1>
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



<h2>Testing & Implementation Steps</h2>

<p>
<img src="https://i.imgur.com/gJwk8Js.png" height="80%" width="80%" alt="Pinging"/>
</p>
<p>
DNS converts computer names to IP address. I attempted to ping(check for connectivity) to "mainframe." There was no connectivity because there is no DNS record for "mainframe."  
</p>
<br />

<p>
<img src="https://i.imgur.com/tpmb2Vi.png" height="80%" width="80%" alt="Create Mainframe DNS record"/>
</p>
<p>
I created an A-Record titled "mainframe." I made the IP Address the same as my static IP Address for my Domain Controller just to ensure I could ping it successfully.
</p>
<br />

<p>
<img src="https://i.imgur.com/wTdB4k0.png" height="80%" width="80%" alt="Successful Ping"/>
</p>
<p>
I was able to ping the "mainframe" after creating the A-Record. 
  
  
  <img src="https://i.imgur.com/7zWb6n9.png" height="80%" width="80%" alt="Changed Mainframe IP Address"/>
</p>
<p>
I changed the IP Address to 8.8.8.8. I wanted to check and see if I would still be able to successfully ping "mainframe."
</p>

<img src="https://i.imgur.com/XNOu0zs.png" height="80%" width="80%" alt="Ping Successful due to local cache"/>
</p>
<p>
 I was able to ping "mainframe" successfully. When I checked the IP Address associated with the ping it was still pointing to the old IP Address from when I intially created the A-Record. The new IP Address is 8.8.8.8. DNS checks the local cache,  then local host file, and lastly checks DNS.
</p>

<img src="https://i.imgur.com/IFEn7qD.png" height="80%" width="80%" alt="Flush DNS"/>
</p>
<p>
I flushed the DNS server to clear the local cache. You have to run the CLI as an admin to flush the DNS server. I wanted to observe what would happen after clearing the local cache. I was able to ping the "mainframe" successfully. The IP Address has been updated to 8.8.8.8. 
</p>
</p>
</p>
</p>
This lab really helped solidify my knowledge of the Domain Name System. I was able to see exactly how the system works in real time.
</p>

