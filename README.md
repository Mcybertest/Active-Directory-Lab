
<h1>Active Directory - Home Lab</h1>

<h2>Description</h2>

In this lab, I created an Active Directory home-lab environment with 1,000+ users on a simulated corporate network. 
<br />


<h2>Prerequisites</h2>

I used the Oracle Virtual Box to power 2 separate virtual machines 
- <b>Windows Server 2019 for the Domain Controller VM </b>
- <b>Windows 10  for the client VM</b>
- <b>A Powerscript script</b>
- <b>Basic Powerscript commands</b> 


<h2>Project walk-through</h2>

<p align="center">
<br> Overview of network infrastructure <br/>
<img src="https://i.postimg.cc/rwRnMxRB/Network-Infrastructure.png" height="80%" width="80%" alt="Network infrastructure diagram"/>
<br />
<br />
I have installed both VMs beforehand. Configure the NICs on the DC virtual machine <br />
- NIC 1 - NAT (this is the route to the internet)
- NIC 2 - INTERNAL (this connects to the internal network)
 <br/>
<img src="https://i.imgur.com/JlQMoa9.png" height="80%" width="80%" alt="network adapters"/>
<br />
<br />
Step 1 - Differentiate between the Network Adapters (network icon on the bottom screen - Ethernet settings - status) <br />
- Adapter 1 with the APIPA - I renamed it *Internet*
- Adapter 2 with IP address 10.0.2.15 - I renamed it *INTERNET*
<br/>
<img src="https://i.postimg.cc/qqG0QGz2/Adpater-names.png" height="80%" width="80%" alt="install srv2019"/>
<br />
<br />
<p align="center">
  I replaced the APIPA address 169.254.17.146 with the following scope, for the internal network
- <b><i>IP address of 172.16.0.1 / Subnet mask 255.255.255.0 / Default Gateway (empty) / DNS - 127.0.0.1 </b></i>   <br/>
<img src="https://i.postimg.cc/ncwTBDQh/Config-Internal-network.png" height="80%" width="80%" alt="Replaces APIPA"/>
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
<img src="https://i.imgur.com/MpduPjd.png" height="80%" width="80%" alt="set dhcp scope"/>
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
<img src="https://i.imgur.com/GfwHrGN.png" height="80%" width="80%" alt="create second vm"/>
<br />
<br />
While testing network connectivity, I realized that I forgot to add the DC router’s IP address to Client1’s DHCP configuration. As a result, there was no default gateway. Let’s fix that
  <br/>
<img src="https://i.imgur.com/qzwW3gG.png" height="80%" width="80%" alt="network connectivity"/>
<br />
I rectified the issue and am now using the ping command to confirm that everything works 
  <br/>
<img src="https://i.imgur.com/buJcmCT.png" height="80%" width="80%" alt="rectified network issue"/>
<br />
  <img src="https://i.imgur.com/48lvxGs.png" height="80%" width="80%" alt="network issue rectified"/>
<br />
 Connect Client1 to the Domain
  <br/>
<img src="https://i.imgur.com/bqHtpRR.png" height="80%" width="80%" alt="connect client 1"/>
<br />
<br />
Client1 is configured correctly 
  <br/>
<img src="https://i.imgur.com/i0a7Cy5.png" height="80%" width="80%" alt="client1 configured"/>
<br />
We can log in using one of the random users created with the .ps1 script 
  <br/>
<img src="https://i.imgur.com/bJAtKPL.png" height="80%" width="80%" alt="new user sign in"/>
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
