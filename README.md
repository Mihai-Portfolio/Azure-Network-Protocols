<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create two virtual machines and ensure they are connected to the same virtual network
- Observe traffic on your computer, such as ICMP, SSH, DHCP, and DNS.
- Perpetually ping the second virtual machine and deny ICMP traffic with the second virtual machine's network sercurity group
- Access the second virtual machine's command line using SSH protocol

<h2>Actions and Observations</h2>

![image](https://github.com/user-attachments/assets/03b9024e-3756-490c-af24-36f6b1de7fe8)

</p>
<p>
Start off by creating two virtual machines. Name the first virtual machine East and run windows 10 with 2cpus. Name the second virtual machine West and run Ubuntu Pro 24.04. To save on cost, run the West virtual machine with just one CPU since it won't be opened. When creating both virtual machines, be sure to connect them to the same location, as well as the same virtual network. In the tutorial, the location is set to Switzerland North and the name of the virtual network is East-West-Virtual-Network. You may choose a different location depending on availability. Once both virtual machines have been created, log into the East virtual machine using remote desktop. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once logged into the East virtual machine, open Microsoft Edge and download Wireshark. Once wireshark is downloaded, open it and filter for only ICMP traffic. Go to Azure and click on the West virtual machine. You will find the West virtual machine's private IP address under the networking section. In this case, the private IP address is 10.0.0.4, however, your private IP address will more than likely be different. Go back to your East virtual machine's remote desktop, ping the West virtual machine's private IP address and observe the traffic. Use the command "ping 10.0.0.4 -t" to preform a perpetual ping to the West virtual machine. To stop the ping from the East virtual machine, open Azure and search for network security groups, and click on West-NSG to open the West virtual machine's network security group. Under settings, click the "Inbound Security Rules" and add in a rule to deny any ICMP traffic from hitting the West virtual machine. Be sure to set the priority to the lowest numbers so no previous rules override this one. Go back to the East virtual machine and observe the traffic timing out. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
