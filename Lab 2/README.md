# FTP Server Configuration

## Introduction

This lab focuses on configuring an FTP server within a local area network using Cisco Packet Tracer. The project demonstrates how users can securely upload and retrieve files from a centralized file server.

The simulation includes two client computers, one DNS server, one FTP server, and a switch used for connectivity.
Objectives

The objectives of this lab are to:

- Configure an FTP server

- Configure DNS services

- Assign static IP addresses

- Create FTP user accounts

- Upload files to the FTP server
- Retrieve files from the FTP server

- Verify network communication using ping

  ---

# Network Components

| Device | Quantity |

| PCs | 2 |

| Switch | 1 |

| DNS Server | 1 |

| FTP Server | 1 |

---

# Network Topology

The network consists of:

- 2 Personal Computers

- 1 Switch

- 1 DNS Server

- 1 FTP Server

All devices were connected using Copper Straight-Through cables.

---

<img width="462" height="390" alt="image" src="https://github.com/user-attachments/assets/f6bc7680-8690-4674-a131-fc343db9758c" />



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

```cmd

ping 172.16.1.15

```
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

<img width="460" height="390" alt="image" src="https://github.com/user-attachments/assets/52f0b637-4b98-4ed5-9905-2b9c128b5f12" />


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

```cmd

ftp 172.16.1.15

```


Enter the username and password for the Sammy account.

Upload the file using:

```cmd

put item.txt

```
output:

```
Writing file items.txt to 172.16.1.15:

File transfer in progress...

[Transfer complete - 1020 bytes]

1020 bytes copied in 0.043 secs

```
Step 9 - Retrieve File Using Jane PC

<img width="400" height="340" alt="image" src="https://github.com/user-attachments/assets/17691713-d74a-4778-8495-e32a319cafc4" />

Open Jane PC.
Navigate to Desktop > Command Prompt

Connect to the FTP server:

```cmd

ftp 172.16.1.15

```
Login using Jane's credentials.

Download the file using:

get items.txt
output:

``` cmd
Reading file items.txt from 172.16.1.15:

File transfer in progress...

[Transfer complete - 1020 bytes]

1020 bytes copied in 0.01 secs

```
Step 10 - Verify Downloaded File

Exit the command prompt.

Open:

Desktop > Text Editor
Click:

File > Open
Select:

items.txt

The transferred file should now be available on Jane PC.
