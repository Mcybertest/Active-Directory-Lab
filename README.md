
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
<img src="https://i.imgur.com/2fyEvRb.png" height="80%" width="80%" alt="Network infrastructure diagram"/>
<br />
<br />
Create a Virtual Machine (VM) for Domain Controller  <br/>
<img src="https://i.imgur.com/PMcLnnq.png" height="80%" width="80%" alt="Create VM"/>
<br />
<br />
Configure 2 network adapters, NAT & Internal <br/>
<img src="https://i.imgur.com/JlQMoa9.png" height="80%" width="80%" alt="network adapters"/>
<br />
<br />
Mount & Install Windows Server 2019 on the DC VM <br/>
<img src="https://i.imgur.com/gs9kDks.png" height="80%" width="80%" alt="install srv2019"/>
<br />
<br />
Assign the following to the internal network
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
 Install and configure NAT & Routing, so Win 10 client on the private network can access the internet through the Domain Controller  
  <br />
<img src="https://i.imgur.com/lm5n7oZ.png" height="80%" width="80%" alt="NAT and routing configuration"/>
<br />
  <br />
Set up DHCP, add scope information, so Win 10 Client can receive an IP address
  <br />
<br />
<img src="https://i.imgur.com/JBym9c0.png" height="80%" width="80%" alt="set dhcp scope"/>
<br />
   <br />
Add users to Active Directory using a .ps1 script
  <br/>
 <br />
<img src="https://i.imgur.com/uLYhb7S.png" height="80%" width="80%" alt="add users"/>
<br /> 
  <br />
Active directory u
  sers are created
  <br/>
 <br />
<img src="https://i.imgur.com/xPRysyJ.png" height="80%" width="80%" alt="created user"/>
<br /> 
<br />
Create second VM for our Win 10 client, network adapter is set to connect to the internal network
  <br/>
<img src="https://i.imgur.com/GfwHrGN.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
<br />
Testing for network connectivity, I realised I forgot to add the DC router’s IP address on the DHCP, hence no default gateway, so let's fix that
  <br/>
<img src="https://i.imgur.com/qzwW3gG.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
Issue rectified, using the ping command to confirm that everything works 
  <br/>
<img src="https://i.imgur.com/buJcmCT.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
  <img src="https://i.imgur.com/48lvxGs.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
 Connect Client1 to the Domain
  <br/>
<img src="https://i.imgur.com/bqHtpRR.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
<br />
Client1 is configured correctly 
  <br/>
<img src="https://i.imgur.com/i0a7Cy5.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
Then, we login with one of the random users created with the .ps1 script 
  <br/>
<img src="https://i.imgur.com/wRHIAt2.png" height="80%" width="80%" alt="Active Directory Installation"/>
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
