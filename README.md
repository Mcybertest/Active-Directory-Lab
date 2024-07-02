
<h1>Active-Directory Home-Lab</h1>

<h2>Description</h2>

In this lab, I set up an Active Directory home-lab environment with over 1,000 users. It simulates a corporate network where client systems communicate within a private network. To access the internet, they must go through an external system (Domain Controller in this project).
<br />


<h2>Languages and Utilities Used</h2>

- <b>Oracle Virtual Box</b>
- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Windows Server 2019</b>
- <b>Windows 10 Client</b>
- <b>2 Virtual Machines</b>

<h2>Project walk-through</h2>

<p align="center">
<br> We aim to simulate this network infrastructure <br/>
<img src="https://i.imgur.com/2fyEvRb.png" height="80%" width="80%" alt="Network infrastructure diagram"/>
<br />
<br />
Create a Virtual Machine (VM) for Domain Controller  <br/>
<img src="https://i.imgur.com/PMcLnnq.png" height="80%" width="80%" alt="Create VM"/>
<br />
<br />
Configure network adapters 1 and 2 to use NAT (Network Address Translation) & Internal, respectively <br/>
<img src="https://i.imgur.com/JlQMoa9.png" height="80%" width="80%" alt="network adapters"/>
<br />
<br />
Mount & Install Windows Server 2019 on the Domain Controller's VM <br/>
<img src="https://i.imgur.com/gs9kDks.png" height="80%" width="80%" alt="install srv2019"/>
<br />
<br />
<p align="center">
  I replaced the APIPA address 169.254.17.146 with the following scope, for the internal network
- <b><i>IP address of 172.16.0.1 / Subnet mask 255.255.255.0 / Default Gateway (empty) / DNS - 127.0.0.1 </b></i>   <br/>
<img src="https://i.imgur.com/VoTVYK3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
First, install and configure Active Directory Domain Services, and then create a dedicated admin account 
  <br/>
<img src="https://i.imgur.com/szGU6Cz.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
<br />
 Install and configure NAT and routing so that the Windows 10 client on the private network can access the internet through the Domain Controller  
  <br />
<img src="https://i.imgur.com/lm5n7oZ.png" height="80%" width="80%" alt="NAT and routing configuration"/>
<br />
  <br />
Set up DHCP and add scope information so that the Windows 10 client can receive an IP address
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
Active directory users are created
  <br/>
 <br />
<img src="https://i.imgur.com/xPRysyJ.png" height="80%" width="80%" alt="created user"/>
<br /> 
<br />
Create a second VM for our Windows 10 client (Client 1), its network adapter is set to connect to the internal network
  <br/>
<img src="https://i.imgur.com/GfwHrGN.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
<br />
While testing network connectivity, I realized that I forgot to add the DC router’s IP address to Client1’s DHCP configuration. As a result, there was no default gateway. Let’s fix that
  <br/>
<img src="https://i.imgur.com/qzwW3gG.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
I have rectified the issue and am now using the ping command to confirm that everything works 
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
We can log in using one of the random users created with the .ps1 script 
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
