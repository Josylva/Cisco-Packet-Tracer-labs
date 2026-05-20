# Network Topology

The network consists of:

- 2 Personal Computers
- 1 Switch
- 1 DNS Server
- 1 FTP Server

All devices were connected using Copper Straight-Through cables.

---

# Devices Used

| Device | Purpose |

| PC-PT (Jane) | FTP Client |

| PC-PT (Sammy) | FTP Client |

| Server-PT (DNS) | DNS Services |

| Server-PT (FTP) | FTP File Server |

| 2960-24TT Switch | Network Connectivity |

---

# Cable Connections

| Device | Switch Port |

| Jane PC | FastEthernet 0/1 |
| Sammy PC | FastEthernet 0/2 |
| DNS Server | FastEthernet 0/3 |
| FTP Server | FastEthernet 0/4 |

---

# IP Addressing Scheme

| Device | IP Address | Subnet Mask | DNS Server |

| DNS Server | 172.16.1.17 | 255.255.0.0 | 172.16.1.17 |

| FTP Server | 172.16.1.15 | 255.255.0.0 | 172.16.1.17 |

| Jane PC | 172.16.1.20 | 255.255.0.0 | 172.16.1.17 |

| Sammy PC | 172.16.1.19 | 255.255.0.0 | 172.16.1.17 |



# Step 1 - Configure the DNS Server

1. Open the DNS Server.

2. Navigate to Desktop menu > IP Configuration:

Configure the following:

IP Address: 172.16.1.17

Subnet Mask: 255.255.0.0

DNS Server: 172.16.1.17

Step 2 - Configure the FTP Server
Open the FTP Server.

Navigate to:

Desktop > IP Configuration
Configure the following:

IP Address: 172.16.1.15

Subnet Mask: 255.255.0.0

DNS Server: 172.16.1.17

Step 3 - Configure Client PCs

Jane PC
Navigate to:

Desktop > IP Configuration

Configure:

IP Address: 172.16.1.20

Subnet Mask: 255.255.0.0

DNS Server: 172.16.1.17

Sammy PC

Navigate to:

Desktop > IP Configuration

Configure:

IP Address: 172.16.1.19

Subnet Mask: 255.255.0.0

DNS Server: 172.16.1.17

Step 4 - Verify Network Connectivity

Use the Command Prompt on both PCs to test connectivity.

Example:

ping 172.16.1.15

If configured correctly, replies from the FTP server should be received successfully.

Step 5 - Configure FTP Services
Open the FTP Server.

Navigate to:

Services > FTP
Ensure the FTP service is turned ON.

Step 6 - Create FTP User Accounts

User Account 1

Username |	Password

jane | foster23

Permissions enabled:

Read, Write, Delete, Rename

User Account 2

Username|	Password

sammy|	sam89

Permissions enabled:

Read, Write, Delete, Rename

Step 7 - Create a File From Sammy PC

Open Sammy PC.

Navigate to:

Desktop > Text Editor
Create a file named:

items.txt
input text

Save and close the text editor.

Step 8 - Upload File to FTP Server
Open:

Desktop > Command Prompt
Connect to the FTP server:

ftp 172.16.1.15

Enter the username and password for the Sammy account.

Upload the file using:

put items.txt

output:

Writing file items.txt to 172.16.1.15:
File transfer in progress...
[Transfer complete - 1020 bytes]
1020 bytes copied in 0.043 secs
Step 9 - Retrieve File Using Jane PC

Open Jane PC.
Navigate to Desktop > Command Prompt

Connect to the FTP server:

ftp 172.16.1.15
Login using Jane's credentials.

Download the file using:

get items.txt
output:

Reading file items.txt from 172.16.1.15:

File transfer in progress...

[Transfer complete - 1020 bytes]

1020 bytes copied in 0.01 secs

Step 10 - Verify Downloaded File

Exit the command prompt.

Open:

Desktop > Text Editor
Click:

File > Open
Select:

items.txt
The transferred file should now be available on Jane PC.
