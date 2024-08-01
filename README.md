
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
<br> - NIC 1 - NAT (this is the route to the internet)<br />
<br> - NIC 2 - INTERNAL (this connects to the internal network)<br />
<img src="https://i.imgur.com/JlQMoa9.png" height="80%" width="80%" alt="network adapters"/>
<br />
<br />
Step 1 - Differentiate between the Network Adapters (network icon on the bottom screen - Ethernet settings - status) <br />
<br> - Adapter 1 with the APIPA - I renamed it *Internet* <br />
<br> - Adapter 2 with IP address 10.0.2.15 - I renamed it *INTERNET* <br />
<br/>
<img src="https://i.postimg.cc/qqG0QGz2/Adpater-names.png" height="80%" width="80%" alt="install srv2019"/>
<br />
<br />
<p align="center">
<br> Assign IP address configuration to the ‘Internal’ adapter<br/>
<br><i>IP - 172.16.0.1</i><br />
<br><i>Subnet mask - 255.255.255.0</i><br />
<br><i>Default gateway - 0</i><br />
<br><I> DNS - 172.16.0.1</i><br />
<br>Alternatively, the loopback address 127.0.0.1 can be assigned to DNS but I used the IP address instead<br />
<img src="https://i.postimg.cc/zXCwj7WX/Adapter-configuration.png" height="80%" width="80%" alt="Replaces APIPA"/>
<br />
<br />
Step 2 - Add Active Directory<br />
<br>Add a server role - install Active Directory<br />
<br>During the post-deployment configuration, add a new forest and the FQDN ‘mydomain.com’ as the root domain name
  <br/>
  <br> Configure, restart the machine and add a dedicated admin account<br />
<img src="https://i.postimg.cc/JzdscHTz/10-Add-a-forest-restart.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
<br />
Step 3 - Install RAS/NAT <br />
<br>This will allow the Client system to remain on the private network but access the internet through the domain controller
  <br />
<img src="https://i.postimg.cc/cLJWdYbL/24-tool-RAS.png" height="80%" width="80%" alt="NAT and routing configuration"/>
<br />
  <br />
Select the Adapter name “Internet” for routing
  <br />
<br />
<img src="https://i.postimg.cc/dttpCFmW/select-internet-adapter-routing.png" height="80%" width="80%" alt="select adapter"/>
<br />
<br />
<u>Step 4</u> - Set up the DHCP Server<br />
<br>This will allow client systems on the private network to receive IP addresses<br />
<br><i>Add DHCP server role and configure with the following scope</i><br />
<br><i>Set an IP range: 172.16.0.100 - 200</i><br />
<br><i>Subnet mask:   255.255.255.0</i><br />
<br><i>No exclusions</i><br />
<br><i>Lease:   8 days</i><br />
<br><i>Router:	172.16.0.1 (the internal NIC’s IP)</i><br />

<br>Authorise DC & Refresh IPv4 to take effect<br />
 <br />
<img src="https://i.postimg.cc/d0KzLyWC/dhcp-scope-config-done.png" height="80%" width="80%" alt="set up DHCP"/>
<br /> 
<br />
<u>Step 5 - Run a Powershell Script</u><br />
<br><i>I used this to add 1000 generated users for the Active Directory</i><br />
<br><i>Open Powershell as an admin and enable the execution policy with the command ‘Set-ExecutionPolicy Unrestricted”</i><br />
<br><i>To navigate to the folder with the script, mine is on the Desktop </i><br />
 <br><i>cd C:\user\username\Desktop\filename</i><br />

<br>Then locate the txt file with the name.txt by typing ls<br />

<br>Then run the script<br />
 <br />
<img src="https://i.postimg.cc/wj5w4bVt/Run-Powershell.png" height="80%" width="80%" alt="run script"/>
<br /> 
<br />
<u>Step 6</u> - Install & Window 10 Client on the VM & Connect to the Domain Controller<br />
<br />Run the installation as usual<br />
<br />Confirm network connectivity by running <i>ipconfig & ping</i><br />
  <br/>
<img src="https://i.postimg.cc/vmc38Hyn/Test-connectivity.png" height="80%" width="80%" alt="test connectivity"/>
<br />
<br />
Rename the PC through “Rename Advanced” and simultaneously join the domain controller
<br/>
<img src="https://i.postimg.cc/0Q7GrzBz/Change-client-PC-name-join-DC.png" height="80%" width="80%" alt="join dc"/>
<br />
The first user has successfully joined the Active Directory Domain<br />
<br>For further testing, I used one of the random names generated to join the Active Directory for the first time <br />
  <br/>
By running the command <i>whoamI</i>, kmarden has successfully joined mydomain.com
<img src="https://i.postimg.cc/9Mq29hdR/Random-user-whoami.png" height="80%" width="80%" alt="whoami"/>
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
