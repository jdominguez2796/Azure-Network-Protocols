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
- Step 3: Initiate an SSH remote session with Ubuntu from the Windows VM.
- Step 4: Observe DHCP traffic with Wireshark.
- Step 5: Observe DNS traffic with Wireshark.

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

Step 3
<p>
<img src="https://i.imgur.com/9z4DuCq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Windows, begin a new packet capture with Wireshark and filter the packets captured by SSH traffic. In command prompt, enter the command "ssh labuser@10.0.0.5". "ssh" is the name of the command "labuser" is the username we are attempting to log in as, "@" means the target machine's IP, and "10.0.0.5" is the IP address of the machine we are attempting to remote into. The command allows to securely obtain remote access to a target machine with the SSH Protocol (Unlike Telnet which is unencrypted and not secure.). We are then prompted to enter credentials. After enterning the credentials, we are connected to the target machine and can use Ubuntu's CLI terminal as if we were using the machine. In wireshark, we can see the exchange of traffic in detail. Some things to point out are that SSH uses port 22 and the initial key exchanges between the two machines that makes the connection secure.
</p>
<br />

Step 4
<p>
<img src="https://i.imgur.com/zh2tQNC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Windows, begin a new packet capture with Wireshark and filter the packets captured by DHCP traffic. In command prompt run the "command ipconfig /renew". The DHCP protocol is used to automatically assign clients connecting to a network an IP address. Essentially what this command does is ask the DHCP server for a new IP address. In the packet capture, we see DHCP traffic. The Windows client asks the DHCP server for an IP with a DHCP Request and the DHCP server replies with the 10.0.0.4 address with a DHCP ACK message. DHCP uses UDP. DHCP servers listen on port 67 and DHCP clients respond on port 68.
</p>
<br />

Step 5
<p>
<img src="https://i.imgur.com/wsLKKiB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Windows, begin a new packet capture with Wireshark and filter the packets captured by DNS traffic. In command prompt run the "nslookup www.google.com". Essentially what this does is ask the DNS server what google's IP address is. In the packet captures we can see the windows client 10.0.0.4 ask the DNS server 168.63.129.16 for google's IP address. We can also see DNS runs on port 53 and in UDP. DNS automatically maps a website to an IP address. Without DNS, we would have to type IP addresses when browsing the internet. This concludes this tutorial.
</p>
<br />
