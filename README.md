
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

<br> Overview of network infrastructure <br/>
<br>
<img src="https://i.postimg.cc/rwRnMxRB/Network-Infrastructure.png" height="80%" width="80%" alt="Network infrastructure diagram"/>
<br />
<br />
I have installed both VMs beforehand so I began with configuring the NICs on the DC virtual machine <br />
<br> - NIC 1 - NAT (routes to the internet)
<br> - NIC 2 - INTERNAL (connects to the internal network)<br />
<br>
<img src="https://i.imgur.com/JlQMoa9.png" height="80%" width="80%" alt="network adapters"/>
<br />
<br />
<b>Step 1</b> - Differentiate between the Network Adapters (network icon on the bottom screen - Ethernet settings - status) <br />
<br> - Adapter 1 with the APIPA - I renamed it <i>Internet</i>
<br> - Adapter 2 with IP address 10.0.2.15 - I renamed it <i>INTERNET</i> <br />
<br/>
<img src="https://i.postimg.cc/qqG0QGz2/Adpater-names.png" height="80%" width="80%" alt="install srv2019"/>
<br />
<br />
<br> Assign IP address configuration to the <i>Internal</i> adapter<br/>
<br><i>IP - 172.16.0.1</i>
<br><i>Subnet mask - 255.255.255.0</i>
<br><i>Default gateway - 0</i>
<br><I> DNS - 172.16.0.1</i><br />
<br>Alternatively, the loopback address 127.0.0.1 can be assigned to DNS but I used the IP address instead<br />
<br><img src="https://i.postimg.cc/zXCwj7WX/Adapter-configuration.png" height="80%" width="80%" alt="Replaces APIPA"/>
<br />
<br />
<b>Step 2</b> - Add Active Directory<br />
<br>Add a server role - install Active Directory<br />
<br>During the post-deployment configuration, add a new forest and the FQDN ‘mydomain.com’ as the root domain name
<br/>
<br> Configure, restart the machine and add a dedicated admin account<br />
<br><img src="https://i.postimg.cc/JzdscHTz/10-Add-a-forest-restart.png" height="80%" width="80%" alt="Active Directory Installation"/>
<br />
<br />
<b>Step 3</b> - Install RAS/NAT <br />
<br>This will allow the Client system to remain on the private network but access the internet through the domain controller
<br />
<br />
<img src="https://i.postimg.cc/cLJWdYbL/24-tool-RAS.png" height="80%" width="80%" alt="NAT and routing configuration"/>
<br />
<br />
Select the Adapter name <b><i>Internet</i></b> for routing
<br />
<br />
<img src="https://i.postimg.cc/dttpCFmW/select-internet-adapter-routing.png" height="80%" width="80%" alt="select adapter"/>
<br />
<br />
<b>Step 4</b> - Set up the DHCP Server<br />
<br>This will allow client systems on the private network to receive IP addresses<br />
<br><i>Add DHCP server role and configure with the following scope</i><br />
<br><i>Set an IP range: 172.16.0.100 - 200</i>
<br><i>Subnet mask:   255.255.255.0</i>
<br><i>No exclusions</i>
<br><i>Lease:   8 days</i>
<br><i>Router:	172.16.0.1 (the internal NIC’s IP)</i><br />

<br>Authorise DC & Refresh IPv4 to take effect<br />
<br />
<img src="https://i.postimg.cc/d0KzLyWC/dhcp-scope-config-done.png" height="80%" width="80%" alt="set up DHCP"/>
<br /> 
<br />
<b>Step 5</b> - Run a Powershell Script<br />
<br> - <i>I used this to add 1000 generated users for the Active Directory</i>
<br> - <i>Open Powershell as an admin and enable the execution policy with the command</i> <b></i>Set-ExecutionPolicy Unrestricted</i></b>
<br> - <i>To navigate to the folder with the script, mine is on the Desktop</i>
<br> - <i>cd C:\user\username\Desktop\filename</i><br />

<br>Then locate the txt file with the name.txt by typing <b><i>ls</i></b><br />

<br>Run the script<br />
 <br />
<img src="https://i.postimg.cc/wj5w4bVt/Run-Powershell.png" height="80%" width="80%" alt="run script"/>
<br /> 
<br />
<b>Step 6</b> - Install & Window 10 Client on the VM & Connect to the Domain Controller<br />
<br />Run the installation as usual<br />
<br />Confirm network connectivity by running <i>ipconfig & ping</i><br />
<br/>
<img src="https://i.postimg.cc/vmc38Hyn/Test-connectivity.png" height="80%" width="80%" alt="test connectivity"/>
<br />
<br />
Rename the PC through <b><i>Rename Advanced</i></b> to join the domain controller<br/>
<br>
<img src="https://i.postimg.cc/0Q7GrzBz/Change-client-PC-name-join-DC.png" height="80%" width="80%" alt="join dc"/>
<br />
<br>The first user has successfully joined the Active Directory Domain<br />
<br>For further testing, I used one of the random names generated to join the Active Directory for the first time <br />
  <br>
By running the command <i>whoamI</i>, kmarden has successfully joined mydomain.com<br />
<br>
<img src="https://i.postimg.cc/9Mq29hdR/Random-user-whoami.png" height="80%" width="80%" alt="whoami"/>
<br />

<h3>Conclusion</h3>
<br>When I join a new organization, my details are added to a batch file that periodically runs to create new users. <b>Client 1</b> in the network diagram above represents my corporate laptop, allowing me to sign in because my details are already on the network.<br />


 
