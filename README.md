<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop
- Command-Line Tools
- Network Protocols (ICMP, SSH, DHCP, DNS, UDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Virtual Machines (VMs) (Windows and Ubuntu Server [Linux])
- Download, Install, and Run Wireshark
- PowerShell (Ping)
- Monitor Internet Control Message Protocol (ICMP) Traffic
- Change VM-2's Firewall Settings and View Changes in PowerShell + Wireshark
- Connect to VM-2 via SecureShell Protocol (SSH) and Monitor SSH Traffic on Wireshark
- Monitor Dynamic Host Configuration Protocol (DHCP) Traffic
- Monitor Domain Name System (DNS) Traffic
- Monitor User Datagram Protocol (UDP) Traffic

<h2>Actions and Observations</h2>

<p align="center">
<img src="https://i.imgur.com/9ERubqL.png" height="70%" width="70%" alt="VMs Created"/>
</p>
<p> Create two Virtual Machines (VMs) in Microsoft Azure. VM-1 will have Operating System (OS) of Windows 10 with the size of 2 virtual computer processing units (vcpus) and 16 GiB memory. VM-2 will have OS of Ubuntu Server also known as Linux with the 2 vcpus and 16 GiB memory. (Make sure the virtual network matches VM-1's.)
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/9Bfi9GY.png" height="70%" width="70%" alt="VM-1 Wireshark"/> 
</p>
<p> Connect to VM-1. Download Wireshark from the Internet, and install it with default settings. Run Wireshark. Choose Ethernet. Select the shark fin icon. 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/UfwcLAJ.png" height="70%" width="70%" alt="Capture Packets"/>
</p>
<p> Here we can view the different protocol traffic taking place. On the tool bar, type "ICMP". It will filter for the Internet Control Message Protocol (ICMP) only. 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/RCMWkw5.png" height="50%" width="30%" alt="Powershell"/> <img src="https://i.imgur.com/fRt3cIY.png" height="50%" width="50%" alt="Powershell"/>
</p>
<p> Collect VM-2's private ip address (10.0.0.5). In VM-1, open up Power Shell. Type "ping 10.0.0.5" and hit Enter (or Return). In Wireshark, we can view the communication between VM-1 and VM-2.  
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/B50rUAo.png" height="50%" width="30%" alt="VM-2's Firewall Settings"/> <img src="https://i.imgur.com/vUtl66l.png" height="80%" width="40%" alt="VM-2's Firewall Settings"/>
</p>
<p> We can change firewall settings to block or permit specific communication from different protocols. Go to Network Security Groups in Microsoft Azure. Select VM-2. In the Inbound Security Rules, Add Rule. Source: Any, Source Port Range: Any (*), Destination: Any, Service: Custom, Destination Port: Protocol ICMP, Action: Denied, Priority: 200, Name: DenyAnyCustomAnyInbound. (Priority is set at 200 to affect before the SSH protocol.)
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/JnQOgCg.png" height="70%" width="40%" alt="PowerShell Change"/> <img src="https://i.imgur.com/cmm5vcA.png" height="70%" width="40%" alt="Wireshark Change"/>
</p>
<p> Go to VM-1. View how changing VM-2’s Firewall affected PowerShell and Wireshark. (PowerShell - Request Timed Out. Wireshark - No Response Found). By changing VM-2 firewall to deny ICMP, VM-2 is essentially blocking VM-1's ping to communicate.  
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/uluQ9M9.png" height="70%" width="40%" alt="Return PowerShell"/> <img src="https://i.imgur.com/2oheare.png" height="70%" width="40%" alt="Return Wireshark"/>
</p>
<p> Go back to the Network Security Groups in Microsoft Azure. Select VM-2. In the Inbound Security Rules, change DenyAnyCustomInbound rule to Allow ICMP traffic, or delete DenyAnyCustomInbound rule. Return to PowerShell and Wireshark to view the changes. 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/p9gXn3T.png" height="70%" width="70%" alt="Connecting to VM-2 Through SSH"/>
</p>
<p> Connect to VM-2 with SSH. Go to Wireshark and change the filter from ICMP to SSH. In PowerShell, type ssh (username created in VM-2)@(VM-2's private ip address). For instance, ssh labuser@10.0.0.5. When prompted to continue connecting, select yes. The next “PS C:\Users\labuser” enter Password created in VM-2. (Note: Your password may not be visible.)
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/oAL48Je.png" height="70%" width="70%" alt="SSH Traffic"/>
</p>
<p> Following the connection to the Ubuntu (Linux) Server, there is a Linux command line "labuser@VM-2: $". Using Linux commands such as "id", "uname -a", and "ls -lasth", we can view this SSH traffic in Wireshark. 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/vLd8e8A.png" height="50%" width="50%" alt="Exit VM-2"/>
</p>
<p> To exit out of VM-2, in the command line type "exit" and click Enter (or Return). The Linux command line returns to VM-1's Window's Command Line of "PS C:\Users\labuser>". 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/c5ESUsc.png" height="80%" width="40%" alt="DHCP Traffic on PowerShell"/> <img src="https://i.imgur.com/JnqIzty.png" height="80%" width="40%" alt="DHCP Traffic on Wireshark"/>
</p>
<p> Monitor DHCP traffic. In Wireshark (VM-1), change the filter from SSH to DHCP. In PowerShell, type "ipconfig /renew". Then, click back into Wireshark to view the DHCP traffic. 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/pJYyz45.png" height="60%" width="40%" alt="DNS Traffic - PowerShell"/> <img src="https://i.imgur.com/fbvkuJx.png" height="70%" width="50%" alt="DNS Traffic in Wireshark"/>
</p>
<p> Monitor DNS Traffic. In Wireshark (VM-1), change the filter from DHCP to DNS. In PowerShell, type "nslookup google.com". Then, go back to Wireshark to view the DNS traffic. 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/V6uHCzc.png" height="43%" width="30%" alt="UDP in PowerShell"/> <img src="https://i.imgur.com/HdcsNFM.png" height="70%" width="50%" alt="UDP in Wireshark"/>
</p>
<p> Monitor UDP Traffic. In Wireshark (VM-1), change the filter from DNS to UDP. In PowerShell, type "nslookup disney.com". Then, go back to Wireshark to view the UDP traffic. In Wireshark, filters can be changed to focus on specific traffic. For instance, changing the filter from DNS to RDP (Remote Desktop Protocol). In order to do this tutorial, RDP was used to establish a connection to the VMs. 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/FF3maz0.png" height="70%" width="70%" alt="Bye"/>
</p>
<br />
