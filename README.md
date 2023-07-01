<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop
- Command-Line Tools
- Network Protocols (SSH, RDH, DNS, HTTP/HTTPS, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create VM (Windows and Linux [Ubuntu])
- Download, Install, and Run Wireshark
- PowerShell 
- Step 4

<h2>Actions and Observations</h2>

<p align="center">
<img src="https://i.imgur.com/9ERubqL.png" height="70%" width="70%" alt="VMs Created"/>
</p>
<p> Create two Virtual Machines (VMs) in Microsoft Azure. VM-1 will have Operating System (OS) of Windows 10 with the size of 2 virtual computer processing units (vcpus) and 18 GiB memory. VM-2 will have OS of Ubuntu also known as Linux with the 2vcpus and 16 GiB memory. (Make sure the virtual network matches VM-1's.)
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
<p> Here we can view the different protocol traffic taking place. On the tool bar, type "ICMP". It will filter the Internet Control Message Protocol only. 
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/RCMWkw5.png" height="50%" width="30%" alt="Powershell"/> <img src="https://i.imgur.com/fRt3cIY.png" height="50%" width="50%" alt="Powershell"/>
</p>
<p> Collect VM-2's private ip address (10.0.0.5). In VM-1, open up Power Shell. Type "ping 10.0.0.5" and hit Enter (or Return). VM-1 communicated with VM-2. Returning to Wireshark, we can view this traffic. 
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />

<p align="center">
<img src="" height="70%" width="70%" alt=""/>
</p>
<p>
Description
</p>
<br />
