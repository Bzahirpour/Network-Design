<h1>Welcome to my Network Design for my Capstone!</h1>
<img src="https://imgur.com/gAF3Mg8.png" height="100%" width="100%"/>
Network Engineering Capstone
Functionality Report
<br>
<br>
<h2>Test Case #1: Device Discovery and Reachability</h2>
 
 The network designed for my capstone includes five separate VLANs: one Management network (VLAN 10) designed to keep the management of networks separate from users, one Main network (VLAN 20) used for internal users, a separate Guest network (VLAN 30) for guest to use with access only to the internet, one IoT network (VLAN 40) to keep less secure IoT devices separate from user data, and a DMZ (VLAN 99) that houses a public facing web server isolated from all internal networks. ACLs restrict traffic between networks. First, let’s take a moment to discuss the most restrictive networks and then build more access from there for the other networks. The DMZ, Guest, and IoT networks only allow internet access, with ACLs blocking access to all private IP ranges. Next, we have the Main network, which has access to the remote site network. In the ACL, we included a line allowing access to the remote site network, followed by the same rule to deny access to all other private IP ranges. Finally, we have the Management network, which was given explicit permit rules that allow it to reach all the management IPs of all network devices, including those in the remote site, followed by explicit denial for all private IPs. All ACLs were attached to the SVI for the VLANS on both layer three switches that act as the default gateways for each VLAN.
 
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  

I’m posting a screenshot of the network because everything is clearly labeled and documented in the network. This includes all device names/functions, VLANs, subnets, network devices, IP addresses used, interfaces for connections, and layer two and three connections.
  
 
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
Ping was heavily used to verify reachability between networks, and out to the internet. Along with these tools, connecting to webservers in different networks and SSH was also used to verify ACLs and reachability. For example, the Guest network, IoT network, and DMZ are all able to reach the internet web server located at the top right of the network diagram located at 100.0.0.2, and a device from the Management network is able to ssh into a network device, but devices in the Main network unable to ssh into the same device.


Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
1.	Ping tests were used to verify the reachability of each intended network and the functionality of ACLs.
2.	Connecting to web servers in different networks was used to verify port forwarding and ACLS, but I’ll demonstrate port forwarding in task 7 of this submission.
3.	SSH was used to verify the ability to manage network devices remotely from the management network.


Ping test used to verify reachability to the remote site from the Main network, while ACLs block access to Guest, IoT, and DMZ networks:
 
Connection to internet web server used to verify internet reachability from the Guest network:
 
SSh is used to verify the ability to manage network devices from the laptop in the management network, followed by a device in the main network unable to reach the same device:

 
 
 
 
 

Test Case #2: Administering an Access Control List for Guest Access 
Your network must utilize an access control list that allows guest access. Guest access should be limited to internet traffic only.
Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  
 
 ACLs were used to limit the Guest, IoT, and DMZ networks to only being able to reach the internet by creating ACLs that deny access to all private IP ranges and applying them to the VLAN interface on each layer three switch that handles inter-VLAN routing. The main network has the same ACLs limiting it, except for being able to reach the subnet of the remote site. Finally, the management network is also blocked from reaching private IP ranges, with the exception of reaching the management IPs of all network devices, along with Vty lines having ACLs that allow only connections from the management VLAN subnet range.
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  
 
  


 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
 As with the last test case, ping was used to verify the functionality of ACLs, along with SSH. The ability to reach web servers and obtain IPs through DHCP was also used.
 
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
 
1.	Ping from each network to each other network.
2.	Ssh from the management network to network devices.
3.	Connection to the internet webserver from each network.

The ACLs:
 
How they are applied:
 
Ping test from Main network to remote site, Guest, IoT, and DMZ networks:
 
Ping used to verify ability to reach internet webserver while ACLs block access to other internal networks from the Guest network:

 
Demonstrating SSH from Management network to network devices:
 
Connecting to the internet web server from the Guest network:
 
 

Test Case #3: Security Compliance—Log-in Banners 
Display a log-in banner when accessing each device on the network. The log-in banner should notify users of an acceptable use policy (AUP) or other security-based policies when attempting to log into the network. 

Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  

The buissness policys mandated the use of log-in banners to display a warning to anyone connecting to the device and informing them of the company’s AUP.
 
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  

Network topology with banners displayed inside of the cli of Dist01:
 
 
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
To test the functionality of the banners, log-in through the CLI and ssh was performed.
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
 
1.	Log in through CLI while providing credentials.
2.	Log in through SSH while providing credentials.
Log in through CLI:
 
Log in through SSH:
 
 

Test Case #4: Accessing External Resources—Routing and Traffic Security 
User devices on your network should have dynamic addresses that are assigned through DHCP unless they provide a service that requires a static address. You must also have at least one network resource that requires a static address. 
Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  
 
The business needed all networks to reach the internet, and the main network needed to reach the remote site through the GRE tunnel. This was achieved through the management of ACLs and NAT.
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  
 
  
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
Ping was used to verify the initial reachability of external resources such as the internet webserver at 100.0.0.2 and Google DNS at 8.8.8.8. In addition, the web browser function of packet tracer was used to demonstrate the ability to connect to the web server through HTTP and HTTPS. Finally, Packet Tracers simulation mode was used to look at the packets as they traversed the network like a Pcap file would be used with Wireshark in a real environment. Simulation mode was used to verify that NAT was working properly. 
 
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
 
1.	Ping to reach external resources.
2.	The web browser functionality of Packet Tracer to connect to the internet web server.
3.	Simulation mode to verify the functionality of NAT.
Because I have already demonstrated the ability to reach external resources through ping and the web browser function of Packet Tracer, I will focus on NAT and the simulation function of Packet Tracer.

Configuration for NAT:
 
“pcap” of ip address translation:
 
 
 

Test Case #5: Layer 2 Link Redundancy and Spanning Tree Protocol (802.1w)  
Enable and manage the Spanning Tree Protocol to establish redundant Layer 2 paths while avoiding possible loops and broadcast storms. Identify the Layer 2 devices that will become the root bridge. 
Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  
 
Spanning tree was used to provide redundant layer two connections while preventing broadcast storms. A full mesh design was used between the distribution and access layers of the network. Dist01 and Dist02 were defined as the root bridge and secondary bridge for each VLAN through the use of ‘spanning-tree vlan “x” root primary’ and ‘spanning-tree vlan “x” root secondary’ commands.
 
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  
 
  
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
 Link lights on the devices were used to initially verify spanning tree topology, as well as checking the status of spanning tree inside of the command line for each switch. 
 
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
 
 
 

1.	Verification through link light status.
2.	Checking running config on the switches.
3.	Checking spanning tree status through cli on the network devices.

Link light status:
 
Running config on Dist01:
 
Running config on Dist02:
 
Output of show span on Dist01:
 
Output of show span on Dist02:
 


 

Test Case #6: Edge Device Syslog and NTP 
Configure perimeter devices to generate system logs that capture unwanted traffic. Additionally, those perimeter devices should utilize Network Time Protocol (NTP) for clock synchronization. 

*NOTE: Packet Tracer's limited logging capabilities can sometimes pose a challenge when trying to simulate a real-world scenario for capturing unwanted traffic and generating system logs. Below are some alternative solutions to satisfying the test case. 

1.	Use an External Syslog Server:
•	Set up a simple syslog server: You can use a Linux machine or a virtual machine to do this. 
•	Configure your Packet Tracer devices: Tell your devices to send their logs to this external server. 
•	Analyze logs: This gives you more flexibility to analyze logs and troubleshoot issues.
•	Document your work.

2.	Focus on ACLs and Verification:
Even though Packet Tracer might not log ACL violations directly, you can still:
•	Configure ACLs: Set up rules to block unwanted traffic.
•	Verify the ACLs: Use Packet Tracer's packet capture or simulation tools to check if the ACLs are working as expected.
•	Document your work: Explain your ACL configuration and the verification process.

Items to be included:
•	Clearly document the limitations of Packet Tracer's logging capabilities.
•	Explain the alternative method used to assess unwanted traffic detection.
•	Emphasize your understanding of the desired logging behavior and how you would implement it in a real-world scenario.

Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  
 
 First, we set up an external syslog server to log inside the management network. Next, we configured our devices to send logging to the syslog server we just configured. Then, we checked the logs on the syslog server to verify functionality. Also, ACLs were used to block unwanted connections from the internet to our network’s WAN router. Specifically, we demonstrated this functionality by blocking Telnet and TFTP. Although Packet Tracer has limited functionality when it comes to syslog, we were still able to show that it is working, at least in theory. This limitation does not allow us to show logs for blocking traffic, but we used simulation mode to demonstrate this traffic being blocked. In a live environment, we would see logs inside the syslog server for this type of traffic being blocked. NTP was configured on the WAN router to an external NTP server; then, distribution switches used the WAN router as their NTP server.
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  
 
  
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
 After configuring the syslog server and logging from the network devices, the syslog was checked to see if it captured logs. ACLs were verified to block malicious traffic through the CLI, and a simulation mode was used to simulate a Pcap. Show NTP association was used to verify the proper use of NTP on WAN routers and distribution switches.
 
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
 
1.	Configured logging on network devices and verified functionality through show run on the network devices and viewing syslog logs.
2.	Verification of ACLs on network device CLI.
3.	Simulation mode Pcap demonstrating malicious traffic being blocked.
4.	Show NTP associations on WAN routers and distribution switches.


Configuration of logging on the network device:
 
Verification of logging on Syslog server:
 



ACL blocking unwanted traffic from WAN connection on ASBR1:
 ”Pcap” showing telnet blocked from the internet webserver to our WAN interface:
  
NTP associations on ASBR1 using external NTP server:
  
NTP associations on Dist01 using ASBR as  NTP server:
 
 

Test Case #7: Basic Network Segmentation at Layer 2 via VLANs and 802.1q 
Your network traffic should be segmented per department or service function at Layer 2 to enhance security and reduce network congestion at the switching layer while allowing segmented traffic to traverse between switches (VLAN trunking).  
Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  
 
The network features five segmented VLANs that meet specific needs that were demonstrated in earlier tasks in this capstone. Trunking and 802.1q encapsulation were utilized to move traffic between VLANs, and in combination with HSRP at the distribution layer, the network features fully redundant trunking and inter-VLAN routing.
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  
 
  
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
Because we already demonstrated the ability to reach other VLANs and networks in earlier tasks in this capstone, this section will focus on trunking, dot1q, and failover. To test functionality failure of devices will be simulated to demonstrate the ability of data to traverse the network in the event of a failure.
 
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
 
 
 
1.	Verify trunks and encapsulation on switches through the use of show interfaces trunk.
2.	Shut all ports on a switch to simulate a failure, showing the other switch becoming active and allowing it to take over the virtual IP so VLAN traffic can be routed.
3.	Show traffic is still able to traverse the network through the use of tracert on a different path.
Verification of trunks and encapsulation on Dist01:
 
Route from Laptop2 in the Main network to the remote site PC before simulating failure:
 
Route from Laptop2 in the Main network to remote site PC post simulating failure:
  

Test Case #8: Basic or Advanced Networking 
Custom Test Case 
Define a custom test case to be run within your network project aligned to your specific organizational need or opportunity identified in Task 1. The custom test case should be equivalent in scope and requirements to the predefined test cases and pertain to basic or advanced networking. 
 
 
 
Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  
 
For test case #8, port forwarding was used to allow access to the DMZ from the internet to reach a public-facing web server. A specific NAT rule was configured on the WAN router (ASBR1) to forward incoming traffic on the WAN interface to the internal webserver. This feature allows the company to host its own public-facing web server while keeping it segmented from all other internal assets. 
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  
 
  
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
 Packet Tracers web browser function was used from the internet web server to the public IP of our company, which connects to our public-facing web server. Pcaps were also used to show NAT performing port forwarding.
 
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
 
1.	Verification of configuration in ASBR1 running-config.
2.	Use the internet webservers browser to try to connect to our companys public facing ip through http. 
3.	Use Pcaps to show address translation occurring during the connection process.



Browser of the internet web server connecting to our company’s public IP:
 
Configuration on ASBR1 translating our companys public ip to our webservers ip:
 
Pcap showing traffic destined for our company’s public IP getting forwarded to our public-facing webserver:
 
 

Test Case #9: IPSec 
Custom Test Case 
Define a custom test case to be run within your network project aligned to your specific organizational need or opportunity identified in Task 1. The custom test case should be equivalent in scope and requirements to the predefined test cases and pertain to IPSec. 
 
 
 
Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  
 
Our company has a remote site that is connected to the main site through a WAN connection. Therefore, the company has decided to use an IPSec tunnel to connect the two sites. Because Packet Tracer does not support the creation of IPSec tunnels, I used a GRE tunnel to simulate this functionality. Static routes were configured to allow traffic to be routed through the tunnel interface for each site.
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  
 
  
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
The CLI was used to check the tunnel configuration for both sites. In addition, a traceroute was used to check the path that the traffic takes to traverse the network from the main site to the remote site.
 
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 




1.	Verification of configuration on the devices tunnel 0 interface.
2.	Trace route from the Main network to the Remote Site network.
 
 Tunnel configuration on ASBR1 with description of how the configuration works:
 
Trace route showing the path the traffic travels from the main site to the remote site, avoiding any public ips because logically the traffic travels through the tunnel:
 
 

Test Case #10: Network Security 
Custom Test Case 
Define a custom test case to be run within your network project aligned to your specific organizational need or opportunity identified in Task 1. The custom test case should be equivalent in scope and requirements to the predefined test cases and pertain to network security. 
 
 
 
Functionality 
Describe the functionality of the test case in relation to your network project. Identify the relevant tools (devices, subnets, etc.) used in this test case and their specific interactions.  
 
For test case #10, our company is demonstrating some of its network security through the use of port security, DHCP snooping, and ARP inspection. The company port security uses a sticky MAC address to learn the MAC of the devices connected to the access ports of our access switches. This allows us to block the port if a device is unplugged from the network and another device is connected to the same port. DHCP snooping allows us to detect and block traffic from any rouge DHCP servers. Arp inspection allows the company to prevent Man-in-the-middle attacks by validating source and destination MAC/IP against the DHCP snooping database.
 
Network Diagram or Segment 
Provide a network diagram or segment visualizing the topology and devices used in this test case.  
 
  
 
Testing Method 
Summarize the testing method used to verify functionality of the network project within the virtual lab environment, including any metrics of success.  
 
We will test port security by changing the mac address of a connected device and showing a port getting disabled. DHCP snooping will be verified by untrusting the port connecting to the DHCP server and requesting a new IP on an end device to simulate the DHCP traffic of a rouge DHCP server getting blocked. Finally arp inspection will be verified by viewing the running configuration on the switch as Packet Tracers arp inspection functionality is limited.
 
Process List 
Provide a comprehensive process list of the steps taken within the network project to run the testing method. Include screenshots to illustrate the process and ensure clarity for others attempting to replicate the test. 
 
1.	Edit the MAC address of a network device to show a port becoming err-disabled, simulating connecting another device with a different MAC address to the port.
2.	Untrusting a port that receives a DHCP packet to simulate what would happen if a rouge DHCP server was connected to an untrusted port.
3.	Verification of configuration and trusted ports on a network device configured with ARP inspection.

Editing the MAC address of Laptop2 caused the interface of the switch to become disabled:
 
Interface F0/2 is err-disabled because of port security:
 
DHCP snooping drops the packet received on an untrusted port:
 
Configuration on Edge01 showing ARP inspection enabled and ports connected to network devices as trusted: 
 
 

Network Troubleshooting 
Discuss how you analyzed the network to identify, troubleshoot, and resolve issues during development or when ensuring functionality of the test cases. 



After applying the ACLs to the VLAN interfaces on the distribution switches, I noticed that SSH was no longer working. Because this occurred after applying the ACLs, I knew they had to be the culprit. So, after reviewing the ACLs, I did not specifically have a rule permitting the devices in the Management network to connect via SSH, so I modified the ACLs to allow the connection to occur.


	Another issue I ran into while working on the project was when writing the ACL to permit SSH traffic to the network devices from the management network, the connection was still being blocked. The rule I added was “permit tcp 10.0.0.0 0.0.0.7 host 10.1.254.2 eq 22”. Let’s break down the rule to better understand the problem “permit tcp 10.0.0.0 0.0.0.7” means allow TCP traffic from the 10.0.0.0/29 network (0.0.0.7 is the wildcard mask for 255.255.255.248). The next part of the ACL is to the “host” at IP address 10.1.254.2, to port 22 (which is the port for SSH). Even when applying this rule to the first line of the ACL, the connection would not work. To troubleshoot the issue, I first removed the rule to verify that the SSH was working properly, which it was. Next, I tried to dissect the rule to see which part was causing the issue. I tried removing the port number, and that didn’t fix it. I tried making the source the host IP instead of the network with a wildcard mask, and that also didn’t work. Next, I removed the TCP and made it IP (all traffic), which didn’t work. After experimenting with this method and not finding a solution, I figured out it was a bug with Packet Tracer. I found a workaround by using a standard ACL rather than an extended one and just making the rule “access-list 99 permit 10.0.0.0 0.0.0.7” making it less specific and applying it to the VTY interface in. This resolved the issue.

	Another problem I faced was that after configuring HSRP on the distribution switches, I noticed my link lights were strobing very fast, so I reviewed simulation mode to look at the Pcap to see what was happening. I realized that HSRP sends packets back and forth to and from the switches to give updates about their status using HSRP packets and ICMP, but my ACLs did not contain any rules allowing this type of traffic, so the network was getting flooded with ICMP failures. To resolve the issue, I edited my ACLs to include rules specifically to allow this type of traffic and restore normal network performance. The rules I added to my ACLs were “permit udp any any eq 1985” and “permit icmp any any”.

I had a blast working on this project and sharing my work. I hope you had as much fun reading my report as I did building the project! Thank you so much for your time and effort!

Benjamin Nissan Zahirpour






















![image](https://github.com/user-attachments/assets/e3b7d7a2-ca70-4533-83f2-f2e93246e21d)
