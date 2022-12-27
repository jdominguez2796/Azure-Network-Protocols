<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from a Windows 10 and Ubuntu Azure Virtual Machine with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Overview of Topology</h2>

<img src="https://i.imgur.com/QdOU3P7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

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

- Step 1: On the Windows 10 VM, begin packet capturing with Wireshark and Ping the Ubuntu machine.
- Step 2: Block inbound ICMP protocol traffic on the Ubuntu VM with an Azure inbound security rule in the Network Security Group Firewall.
- Step 3
- Step 4

<h2>Actions and Observations</h2>

Step 1
<p>
<img src="https://i.imgur.com/NJPakcS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the Windows 10 VM, open Wireshark and begin a packet capture by selecting the blue wireshark icon on the top left. Filter the traffic captured by the "icmp" protocol. Open command prompt and ping the Ubuntu VM's IP with the command "ping 10.0.0.5". Observe the 8 packets captured. Ping uses the ICMP protocol hence why we filtered by "icmp". Ping is commonly used to test network connectivity between devices on a network. We sent 4 ICMP Echo requests from the Windows VM to the Ubunto VM and received 4 ICMP Echo replys confirming connectivity. 
</p>
<br />

Step 2
<p>
<img src="https://i.imgur.com/g2636hD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the Windows VM command prompt, run the command "ping 10.0.0.5 -t". Adding the -t option makes the ping take action an infinte amount of times. In Azure, navigate to the Ubuntu VM and expand the networking option. Select "add inbound port rule" and create a rule for the firewall denying all incoming ICMP protocol traffic. Back to the Windows VM, observe the ping commands beginning to fail. They are failing because the Windows VM is not receiving an ICMP echo reply from the Ubuntu VM. Ubuntu is not replying because the firewall rule we added prevents Ubuntu from event receiving the Windows ICMP echo request. This makes ping a useful troubleshooting tool. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
