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

![image](https://github.com/user-attachments/assets/9aa1bc0e-0cbf-4c37-b1da-14e316ed3cdf)
![image](https://github.com/user-attachments/assets/e3b803a9-001b-47cb-a130-f72c6bb87351)



</p>
<p>
Start off by creating two virtual machines. Name the first virtual machine East and run windows 10 with 2 vCPUs. Name the second virtual machine West and run Ubuntu Pro 24.04. To save on cost, run the West virtual machine with just one CPU since it won't be opened. Be sure to connect both virtual machines to the same resourse group and the same location. In this case, the resourse group is Network-Protocols and the location is Switzerland North. However, you may choose a different location depending on availability.

 ![image](https://github.com/user-attachments/assets/300fe509-1088-4dd8-8ebb-76293ea824a8)

Be sure to connect both virtual machines to the same virtual network. It's important to note that it may take up to 15 minutes for your virtual network to be created. In the tutorial, the name of the virtual network is East-West-Virtual-Network. Once both virtual machines have been created, open remote desktop and log into the East virtual machine using its public IP address. 
</p>
<br />

![image](https://github.com/user-attachments/assets/fc444b2b-b04b-4ca0-aca7-e07be7e782ec)
![image](https://github.com/user-attachments/assets/7bea212f-de04-4599-824a-0d39b639010e)

![image](https://github.com/user-attachments/assets/4a3d08ba-7574-4b81-a87d-2ce057a96ef1)



</p>
<p>
Once logged into the East virtual machine, open Microsoft Edge and download Wireshark (https://www.wireshark.org/download.html). Once wireshark is downloaded, open it and observe traffic. Go to Azure and click on the West virtual machine. You will find the West virtual machine's private IP address under the networking section. In this case, the private IP address is 10.0.0.5, however, your private IP address will more than likely be different. Go to the East virtual machine's rempote desktop and fileter wireshark's traffic to ICMP traffic only. Ping the West virtual machine's private IP address and observe the traffic.

![image](https://github.com/user-attachments/assets/bed63514-438e-4174-a36b-923bfd9c66f5)
![image](https://github.com/user-attachments/assets/cf616abf-0e05-4121-a27d-c482ca035d2e)

![image](https://github.com/user-attachments/assets/23c512da-0936-4ce9-8b6f-3341a7a2ee27)


  
  Go back to your East virtual machine's remote desktop, ping the West virtual machine's private IP address and observe the traffic. Use the command ping 10.0.0.5 -t to preform a perpetual ping to the West virtual machine. To stop the ping from the East virtual machine, open Azure and search for network security groups, and click on West-NSG to open the West virtual machine's network security group. Under settings, click the "Inbound Security Rules" and add in a rule to deny any ICMP traffic from hitting the West virtual machine. Be sure to set the priority to the lowest numbers so no previous rules override this one. Go back to the East virtual machine and observe the traffic timing out. 
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/3650bd57-004e-4e7b-9eea-c273299bd087)
![image](https://github.com/user-attachments/assets/25346006-2fbe-4696-bdb3-b334c9c04061)

</p>
<p>
SSH into the West virtual matchine with the East virtual machine by typing "ssh (username)@(private IP address of the West virtual machine). In this case, the command would be "ssh player1@10.0.0.5". Once entered, it will ask if you want to continue connecting and you'll have to type "yes". Next, it'll ask you for the password you made when creating the virtual machine. It's important to note that your password will not display on the screen when typing. Once the password is entered, you will be in the West virtual machine's command line. Since the West virtual machine is running on Linux, use Linux commands to interact with the West virtual machine such as id, uname -a, and pwd. Oberserve the traffic in Wireshark and notice how things like the operating system, user and IP address in the command line are from the West virtual machine. Type "exit" to end SSH connection. 
</p>
<br />

![image](https://github.com/user-attachments/assets/5b234278-4f84-49a8-acf4-a38ab461bcbf)
![image](https://github.com/user-attachments/assets/f232f246-7fd3-49c9-a83a-923db1664fdb)
![image](https://github.com/user-attachments/assets/f8ee284f-1e22-411a-b63a-efac9bbafb81)

In Wireshark, filter the traffic to show only DHCP traffic. Then, open the command line and type "ipconfig /renew". Observe traffic being sent to and from your virtual machine. Next, filter for DNS traffic. Once the traffic is filtered, open the command line and type "nslookup www.amazon.com)" to find the IP address of Amazon. Observe the DNS traffic in Wireshark. One interesting protocol to filter is RDP. Since we're using RDP for the East virtual machine, there is a vast amount of traffic being sent to and from the East virtual machine and the computer you're using for RDP. 




***Be sure to delete your virtual machines in Azure at the end of the tutorial so you don't have to pay for something you're not using***
