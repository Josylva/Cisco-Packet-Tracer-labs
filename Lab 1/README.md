
DHCP SERVER CONFIGURATION
===============================

This project demonstrates the configuration and implementation of a DHCP-based Local Area Network (LAN) using Cisco Packet Tracer. The network was designed to automate IP address assignment for multiple client devices connected through a switch.

-------------------------------
NETWORK DEVICES USED
-------------------------------

- 1 Server

- 1 Switch

- 3 Personal Computers (PC0, PC1, PC2)

- Copper Straight-Through Cables

-------------------------------
SERVER CONFIGURATION
-------------------------------

The server was configured as the DHCP server responsible for dynamically assigning IP addresses to all connected client devices.

Server IP Address: 192.168.1.15

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.1.100

Starting DHCP IP Address: 192.168.1.8

The DHCP service was enabled on the server to automatically distribute IP configuration information including:

- IP Address

- Subnet Mask

- Default Gateway

-------------------------------
SWITCH PORT CONNECTIONS
-------------------------------

The devices were connected to the switch using the following FastEthernet ports:

PC0  ---> FastEthernet 0/1

PC1  ---> FastEthernet 0/2

PC2  ---> FastEthernet 0/3

Server ---> FastEthernet 0/4

-------------------------------
DHCP Server 
-------------------------------
Navigate to the server that was configured to act as the DHCP server for the network.

Step 1 — Configure Server IP Address

Click on the server device.

Navigate to the Config tab.

Select FastEthernet0.

Assign a static IPv4 address to the server.

Example configuration: 192.168.1.15


Navigate to the services menu and turn on the DHCP service, Input start IP address and subnet mask.

<img width="460" height="380" alt="image" src="https://github.com/user-attachments/assets/9dcd423c-3418-476d-b2b8-eb26dfef3359" />


-------------------------------
REQUESTING IP ADDRESS USING CMD
-------------------------------

To request an IP address dynamically from the DHCP server, the following command was executed from the Command Prompt on each PC:

```cmd
ipconfig /renew
```

This command forces the client computer to send a DHCP request to the server and obtain a valid IP address automatically.

IP address assigned are as follows:

PC0

Interface: FastEthernet 0/1

Assigned IP Address: 192.168.1.8

PC1

Interface: FastEthernet 0/2

Assigned IP Address: 192.168.1.9

PC2

Interface: FastEthernet 0/3

Assigned IP Address: 192.168.1.10

<img width="460" height="380" alt="image" src="https://github.com/user-attachments/assets/359f014c-e844-43e4-9b41-7f762dbe0a9c" />


-------------------------------
TESTING NETWORK CONNECTIVITY
-------------------------------

Connectivity between devices was tested using the ping command.

Example:

From PC1 (192.168.1.9), the ping command was used to test communication with PC0 (192.168.1.8):

```cmd
ping 192.168.1.8
```

Successful replies confirmed that:
- DHCP configuration was working correctly

- Devices could communicate across the LAN

- The switch connections were properly configured
