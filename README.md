Steps to Set Up a Network:

1.	Add End Devices:
- Include devices like laptops, PCs, printers, and servers.
- In Packet Tracer, select "End Devices" from the bottom left and choose the desired devices from the available options.
2.	Add a Switch and Connect Devices:
- A switch connects hosts within the same local area network (LAN).
-	In Packet Tracer, go to "Network Devices" > "Switches," and use a "Copper-Straight Through" cable to connect the switch to end devices.
- Click the switch, select an ethernet port (e.g., Fast Ethernet 0/1), then connect it to an end device. Repeat for all devices.
4.	Configure IPv4 Addresses:
- Assign IP addresses to each device.
- In Packet Tracer, click on a device, go to "Config," and under "Interface" > "Fast Ethernet 0," set it to static. Input the IPv4 address and subnet mask.
- Prioritize IP addresses, starting with the switch, router, and then end devices. For example, use 192.168.0.0/26 and 172.16.0.0/24 for available IP addresses.
5.	Add a Router:
- Routers connect LANs to external networks, like the internet.
- In Packet Tracer, click the router, turn it on (using the power button), and use a "Copper-Straight Through" cable to connect it to the switch.
6.	Set the Default Gateway:
- The default gateway is the router’s IP address, guiding traffic when the server is unreachable. Set this for all devices to enable proper communication.
7.	Test the Connection with a Ping:
- After setting up the network, test communication by pinging devices.
- In Packet Tracer, go to "Desktop" > "Terminal" and use the "ping" command to test connectivity.
8.	Configure a DNS Server:
- The DNS server resolves domain names to IP addresses, enabling devices to locate web resources.
- Set up a DNS server using a tool like NAMO (MAMP). Configure the server and test by accessing a webpage from another device.

FAQ
- Why can't I ping between devices on different LANs?
Common Issue:
Devices on different LANs cannot communicate with each other via ping.
Possible Cause:
The router interfaces might be misconfigured, or the devices might not have the correct default gateway.
Troubleshooting Steps:
1.	Check the IP address configuration on the router interfaces using show ip interface brief to ensure they are properly assigned and up/up.
2.	Verify that the devices have the correct default gateway configured (e.g., on LAN 1, the default gateway should be the router interface IP 192.168.0.1).
3.	Ensure that the devices on both LANs are connected to the correct switch ports and that the switch ports are active.
•	Best Practice: Always verify the router interface IP configuration and ensure that each LAN has the appropriate default gateway.
•	Tips for Maintenance: Regularly check the status of your router interfaces and device connections, and ensure that the IP addressing scheme is documented and followed consistently.

2. Why is the DNS server not resolving domain names?
Common Issue:
The DNS server is not resolving domain names, resulting in failure when trying to access websites via domain names.
Possible Cause:
The DNS service might not be enabled, or DNS records may not be configured properly.
Troubleshooting Steps:
1.	Access the DNS server’s configuration and ensure the DNS service is enabled (Services > DNS > On).
2.	Verify that the correct A record is added for the domain you are trying to resolve (e.g., www.example.com pointing to 172.16.0.5).
3.	Make sure the DNS server’s IP address is configured correctly and can be reached by other devices on the network.
   
Best Practice: Always ensure DNS records are configured correctly before deploying the server and test domain resolution from various devices on the network.

Tips for Maintenance: Periodically review the DNS server's A records and add new records as necessary when expanding services. Regularly test DNS resolution to prevent downtime.

3. Why can't I access the web server using the domain name?
   
Common Issue:
Devices cannot access the web server using its domain name, even though the DNS server is running.

Possible Cause:
Either DNS resolution is failing, or the web server's HTTP service is not enabled.

Troubleshooting Steps:
1.	Confirm that the DNS server is resolving the domain name correctly by pinging the domain from a client device:
ping www.example.com
2.	If DNS resolution is working, verify that the web server’s HTTP service is enabled (Services > HTTP > On).
3.	Check that the web server is reachable by its IP address by pinging it directly:
ping 172.16.0.5
•	Best Practice: Make sure the HTTP service on the web server is enabled and that the DNS server correctly points to the web server's IP address.
•	Tips for Maintenance: Regularly test the HTTP service and DNS resolution, especially after making changes to the network or adding new devices. Ensure the web server's configuration is backed up and consistent.

4. The switch cannot ping devices on other networks. What’s wrong?
   
Common Issue:
The switch cannot communicate with devices outside its local network.

Possible Cause:
The switch may not have a default gateway configured, preventing it from routing traffic beyond its own network.

Troubleshooting Steps:
1.	Check the default gateway configuration on the switch by accessing its CLI and using the following command:
show ip interface brief

2.	If the default gateway is missing or incorrect, configure it using:
ip default-gateway 192.168.0.1

3.	Ensure that the switch is physically connected to the correct router interface and that the router is properly routing traffic between networks.
•	Best Practice: Always set the correct default gateway on switches to enable communication with devices outside the local network.
•	Tips for Maintenance: Periodically review the default gateway configuration on all switches, especially when the network topology changes or new devices are added.

5. How do I save the configuration so it persists after a reboot?
   
Common Issue:
Changes made to the network device configuration are lost after rebooting the device.

Possible Cause:
The configuration was not saved to the startup configuration, causing the router or switch to revert to its previous settings after rebooting.

Troubleshooting Steps:
1.	After completing your configuration changes, enter privileged EXEC mode (enable) on the device.
2.	Save the running configuration to the startup configuration using one of the following commands:
Copy code
write memory
or
copy running-config startup-config
•	Best Practice: Always save configurations after making changes to routers or switches to avoid losing them after a reboot.
•	Tips for Maintenance: Regularly back up configuration files to a remote location and ensure that changes are saved immediately after making them.



Best Practices:
1.	Document your Network Configuration: Maintain an up-to-date diagram of your network topology, including IP addresses, VLANs, and default gateways.
2.	Regular Testing: Frequently test your DNS and web server configurations to ensure they are operational.
3.	Save Configurations: Always save changes on network devices to avoid losing them during power outages or reboots.
Tips for Maintaining or Modifying the System:
1.	Scaling the Network: If you need to expand the network, ensure that you properly plan the IP address allocation and subnetting.
2.	Monitor System Health: Implement monitoring tools to track device performance and network connectivity. This will allow for proactive maintenance.
3.	Update Firmware: Regularly check for firmware updates on routers and switches to ensure your network devices are secure and performing optimally.

Retrospective 

I would like to start mentioning that this was my first time building a local area network that connects another local area network trough a router. It blows my mind that I’m capable of doing this almost without any help. During this project, I encountered different challenges, learned a lot of new stuff and a better understanding of the skills I should develop or acquire to improve my future works. The experience was both rewarding and frustrating, as I began creating a functional network I encountered the following challenges. 

Hardware Challenge

One of the challenges my group and I faced during class was related to hardware setup. Although this wasn’t part of the final project, it deserves an honorable mention. We had correctly set up the end devices, the switch, and the router, but we were unable to establish a connection between the LAN and the router. After spending about 20 minutes troubleshooting, one of us suggested checking the Ethernet ports. It turned out that we had connected the Ethernet cable to the wrong port, which was preventing the switch and router from communicating. Once we corrected the cable placement, the connection was established, and the LAN was functioning properly.

DNS Server, IP Addresses, and Web Server Challenges

While working on the project, I encountered a few challenges, particularly with configuring the router, DNS server, and web server. Setting up the LAN and assigning the correct IP addresses to the end devices went smoothly, but I hit a roadblock when it came to configuring the router. I couldn’t recall the exact commands we had used in class to configure it. To resolve this, I referred to several class slides and online tutorials. With these resources, I managed to configure the router successfully. The next challenge was setting up the DNS server and web server. During class, my role in the group was focused on the web server, so I had little experience with configuring the DNS server. Initially, I wasn’t sure where to begin. However, I revisited the project materials and watched tutorials to guide me through the DNS server setup. I followed the instructions step by step, configured the A records, and was able to get the DNS server to resolve domain names. Through persistence and the help of external resources, I overcame both challenges and completed the setup.

New Skills and Insights Gained

This project gave me practical experience in basic network design, particularly in setting up routers and switches for multi-LAN communication. I learned how to assign IP addresses and configure router interfaces, which are critical skills for network setup. I gained insight into routing and its role in connecting devices across different subnets. I also developed a better understanding of DNS and web server setup, particularly in linking domain names to IP addresses and managing client-server architectures. These skills will be useful in future projects involving network services. Troubleshooting skills were another key takeaway. The project required methodical problem-solving to diagnose connectivity issues. I learned the value of step-by-step verification of configurations, from checking IP addresses to ensuring that essential services like DNS and HTTP are active.

Areas for Improvement

One area where I identified a need for improvement is in my understanding of the theoretical aspects of the project. While I was able to complete the practical setup through hands-on work, I realized that my grasp of the underlying concepts—such as routing protocols, DNS configurations, and network services—was not as strong as it could be. This gap in theory sometimes slowed me down when it came to troubleshooting and understanding why certain configurations weren’t working as expected. I plan to dedicate more time to studying the theoretical components of networking.


