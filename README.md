
<h1>Active-Directory-Lab</h1>

<h2>Description</h2>
In this lab, I created an Active Directory home-lab environment with 1000 users on a virtual machine. I designed a mini corporate network, where the domain controller resides on the external network and the client system on the internal network.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Oracle Virtual Box</b>
- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Windows Server 2019</b>
- <b>Windows 10 Client</b>

<h2>Project walk-through:</h2>

<p align="center">
<br>Overview: Network Infrastructure <br/>
<img src="https://i.imgur.com/2fyEvRb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Create a Virtual Machine (VM) for Domain Controller  <br/>
<img src="https://i.imgur.com/PMcLnnq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Configure 2 network adapters, NAT & Internal <br/>
<img src="https://i.imgur.com/w7oLXBi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Mount & Install Windows Server 2019 on the DC VM <br/>
<img src="https://i.imgur.com/yX8YKaZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
From left to right of the image, the ‘Internal network’ had an APIPA address of 169.254.17.146
I assigned the following to the internal network
- IP address of 172.16.0.1
- Subnet mask 255.255.255.0
- Default Gateway <empty> 
- DNS - 127.0.0.1   <br/>
<img src="https://i.imgur.com/VoTVYK3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Install, configure Active Directory Domain Services, and create a dedicated admin account. 
  <br/>
<img src="https://i.imgur.com/szGU6Cz.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
<br />
 Install and configure NAT & Routing, so Win 10 client residing on the private network can access the internet through the Domain Controller  
  <br/>
<img src="https://i.imgur.com/lm5n7oZ.png" height="80%" width="80%" alt="NAT and routing configuration"/>
<br />
  <br />
Set up DHCP, add scope information, so Win 10 Client can receive an IP address.
  <br/>
<br />
<img src="https://i.imgur.com/JBym9c0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
 <br />
<img src="https://i.imgur.com/HTEs7Gd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br /> 

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
