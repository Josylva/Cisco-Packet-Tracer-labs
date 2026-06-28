# Hotel Network Security: SSH Remote Management and Switch Port Security

## Overview

This project demonstrates the implementation of network security within a multi-floor hotel environment using Cisco Packet Tracer. The network consists of three floors connected through Cisco routers running OSPF routing. Each floor contains multiple VLANs representing different hotel departments.

---

# Objectives

- Configure SSH for secure remote router management
- Generate RSA encryption keys
- Create local user authentication
- Enable SSH-only remote access
- Configure switch port security
- Restrict switch ports to authorized devices
- Use Sticky MAC learning
- Verify SSH connectivity
- Verify switch port security configuration

---

# Network Topology

<img width="680" height="360" alt="image" src="https://github.com/user-attachments/assets/056b66cc-f808-477a-ba35-837566d5abea" />


The hotel network consists of three interconnected floors.

## Floor 1

Departments

- Reception (VLAN 80)
- Logistics (VLAN 60)
- Store (VLAN 70)

Equipment

- Cisco 2901 Router
- Cisco 2960 Switch
- Wireless Access Point
- PCs
- Printers
- Smartphones
- Laptop

---

## Floor 2

Departments

- Sales (VLAN 30)
- HR (VLAN 40)
- Finance (VLAN 50)

Equipment

- Cisco 2901 Router
- Cisco 2960 Switch
- Wireless Access Point
- PCs
- Printers
- Smartphones
- Tablet

---

## Floor 3

Departments

- IT (VLAN 10)
- Administration (VLAN 20)

Equipment

- Cisco 2911 Router
- Cisco 2960 Switch
- Wireless Access Point
- PCs
- Printers
- Smartphones
- Laptop

---
<img width="680" height="460" alt="image" src="https://github.com/user-attachments/assets/9f3bcee6-1136-4d99-b989-d91ca0c552ee" />

---
# Technologies Used

- Cisco Packet Tracer
- SSH (Secure Shell)
- RSA Encryption
- Local User Authentication
- VLANs
- OSPF Routing
- Switch Port Security
- Sticky MAC Address Learning

---
## 🖥️ Department Layout

| Floor | Departments | VLAN | Network IP |
|-------|-------------|------|-------------|
| **1** | IT, Admin | VLAN 10, VLAN 20 | 192.168.1.0/24, 192.168.2.0/24 |
| **2** | Sales, HR, Finance | VLAN 30, VLAN 40, VLAN 50 | 192.168.3.0/24, 192.168.4.0/24, 192.168.5.0/24 |
| **3** | Reception, Store, Logistics | VLAN 80, VLAN 70, VLAN 60 | 192.168.8.0/24, 192.168.7.0/24, 192.168.6.0/24 |

> Each department has atleast **1 PC + 1 Printer**.

---

## Router Configuration

## Floor 3 Router

```bash
Router> enable
Router# configure terminal
Router(config)# interface se0/2/0
Router(config-if)# no shutdown
Router(config-if)# clock rate 64000
Router(config)# interface se0/2/1
Router(config-if)# no shutdown
Router(config-if)# clock rate 64000
Router(config)# interface gig0/0
Router(config-if)# no shutdown
Router(config)# do write
```

## Floor 1 Router
```bash

Router> enable
Router# configure terminal
Router(config)# interface se0/2/0
Router(config-if)# no shutdown
Router(config)# interface se0/2/1
Router(config-if)# no shutdown
Router(config)# interface gig0/0
Router(config-if)# no shutdown
Router(config)# do write
```

## Floor 2 Router

```bash
Router> enable
Router# configure terminal
Router(config)# interface se0/2/0
Router(config-if)# no shutdown
Router(config)# interface se0/2/1
Router(config-if)# no shutdown
Router(config-if)# clock rate 64000
Router(config)# interface gig0/0
Router(config-if)# no shutdown
Router(config)# do write

```

## Floor 1 Switch
```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface range fa0/2-3
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 80
Switch(config)# interface range fa0/5-7
Switch(config-if-range)# switchport access vlan 70
Switch(config)# interface range fa0/4-6
Switch(config-if-range)# switchport access vlan 60
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode trunk
Switch(config)# do write
```

## Floor 2 Switch

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface range fa0/2-3
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 40
Switch(config)# interface range fa0/4-5
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 50
Switch(config)# interface range fa0/6-7
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 30
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode trunk
Switch(config)# do write
```

## Floor 3 Switch

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface range fa0/2-3
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config)# interface range fa0/4-6
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode trunk
Switch(config)# do write
```

## Router IP Address Configuration

## Floor 3 Router
```bash
Router(config)# interface se0/2/0
Router(config-if)# ip address 10.10.10.6 255.255.255.252
Router(config)# interface se0/2/1
Router(config-if)# ip address 10.10.10.2 255.255.255.252
Router(config)# do write
```

## Floor 2 Router
```bash
Router(config)# interface se0/2/0
Router(config-if)# ip address 10.10.10.1 255.255.255.252
Router(config)# interface se0/2/1
Router(config-if)# ip address 10.10.10.10 255.255.255.252
Router(config)# do write
```
# Floor 1 Router

```bash
Router(config)# interface se0/2/0
Router(config-if)# ip address 10.10.10.5 255.255.255.252
Router(config)# interface se0/2/1
Router(config-if)# ip address 10.10.10.9 255.255.255.252
Router(config)# do write
```

# Inter-VLAN Routing & DHCP Configuration

## Floor 3 Router

```bash
Router(config)# interface gig0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.2.1 255.255.255.0
Router(config)# interface gig0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.1.1 255.255.255.0

! DHCP Pools
Router(config)# service dhcp
Router(config)# ip dhcp pool Admin
Router(dhcp-config)# network 192.168.2.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.2.1
Router(dhcp-config)# dns-server 192.168.2.1
Router(config)# ip dhcp pool IT
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 192.168.1.1
Router(config)# do write
```

# OSPF Configuration
## Floor 1 Router
```bash
Router(config)# router ospf 10
Router(config-router)# network 10.10.10.4 255.255.255.252 area 0
Router(config-router)# network 10.10.10.8 255.255.255.252 area 0
Router(config-router)# network 192.168.8.0 255.255.255.0 area 0
Router(config-router)# network 192.168.7.0 255.255.255.0 area 0
Router(config-router)# network 192.168.6.0 255.255.255.0 area 0
Router(config-router)# do write
```

## Floor 2 Router

```bash
Router(config)# router ospf 10
Router(config-router)# network 10.10.10.0 255.255.255.252 area 0
Router(config-router)# network 10.10.10.8 255.255.255.252 area 0
Router(config-router)# network 192.168.4.0 255.255.255.0 area 0
Router(config-router)# network 192.168.3.0 255.255.255.0 area 0
Router(config-router)# network 192.168.5.0 255.255.255.0 area 0
Router(config-router)# do write
```
## Floor 3 Router
```bash
Router(config)# router ospf 10
Router(config-router)# network 10.10.10.0 255.255.255.252 area 0
Router(config-router)# network 10.10.10.4 255.255.255.252 area 0
Router(config-router)# network 192.168.1.0 255.255.255.0 area 0
Router(config-router)# network 192.168.2.0 255.255.255.0 area 0
Router(config-router)# do write
```
## 📶 Access Point Configuration

### Floor 1 Access Point
- **SSID:** Floor1  
- **Password:** floor1@123  
- **Connected Devices:**
  - 1 Laptop
  - 2 Smartphones

### Floor 2 Access Point
- **SSID:** Floor2  
- **Password:** floor2@123  
- **Connected Devices:**
  - 1 Laptop
  - 3 Smartphones
  - 1 Tablet

### Floor 3 Access Point
- **SSID:** Floor3  
- **Password:** floor3@123  
- **Connected Devices:**
  - 1 Laptop
  - 2 Smartphones

---
# Configure SSH on the Routers

SSH provides encrypted remote access to Cisco devices, replacing the insecure Telnet protocol.

The same configuration is applied to both the Floor 1 and Floor 2 routers.

---

## Floor 2 Router Configuration

Enter privileged mode:

```bash
enable
configure terminal
```

Configure the hostname:

```bash
hostname F2-Router
```

Configure the domain name:

```bash
ip domain-name stack
```

Create a local administrator account:

```bash
username stack password stack
```

Generate RSA keys:

```bash
crypto key generate rsa
```

Choose:

```text
Key Size: 1024 bits
```

Configure the VTY lines:

```bash
line vty 0 15
login local
transport input ssh
```

Save the configuration:

```bash
do write
```

---

## Floor 1 Router Configuration

Repeat the same configuration.

```bash
enable
configure terminal

hostname F1-Router

ip domain-name stack

username stack password stack

crypto key generate rsa
```

Select:

```text
1024-bit RSA key
```

Configure SSH:

```bash
line vty 0 15

login local

transport input ssh
```

Save:

```bash
do write
```

---

# Verify SSH Configuration

From any PC on the network, open:

```text
Desktop → Command Prompt
```

Connect to the Floor 2 router:

```bash
ssh -l stack 10.10.10.1
```

You can also connect using any router interface IP address.

Example:

```bash
ssh -l stack 192.168.7.1
```

After entering the password:

```text
stack
```

You should successfully access the router CLI remotely.

---

# Configure Switch Port Security

To prevent unauthorized devices from connecting to the network, Port Security is configured on the Floor 3 switch.

Navigate to:

```bash
enable
configure terminal
```

Select the interface connected to the Test PC:

```bash
interface FastEthernet0/6
```

Enable Port Security:

```bash
switchport port-security
```

Allow only one device:

```bash
switchport port-security maximum 1
```

Enable Sticky MAC learning:

```bash
switchport port-security mac-address sticky
```

Specify the action if another device connects:

```bash
switchport port-security violation shutdown
```

Save the configuration:

```bash
do write
```

---

# Verify Port Security

Use:

```bash
show port-security
```

Expected output:

```text
Secure Port      : Fa0/6
Maximum MACs     : 1
Violation Mode   : Shutdown
Sticky MAC       : Enabled
```

This confirms that only the first learned MAC address is permitted on the port.

---

# Verify Router SSH Configuration

Display the running configuration:

```bash
show running-config
```

or

```bash
show startup-config
```

You should verify the following settings:

- Local username configured
- Domain name configured
- RSA keys generated
- SSH enabled
- VTY lines configured for SSH only
- `login local` enabled

Example:

```text
username stack password stack

ip domain-name stack

line vty 0 4
 login local
 transport input ssh

line vty 5 15
 login local
 transport input ssh
```

---

# Network Features Demonstrated

- Secure remote administration using SSH
- RSA public-key encryption
- Local user authentication
- VLAN-based departmental segmentation
- OSPF dynamic routing
- Switch Port Security
- Sticky MAC Address Learning
- Unauthorized device protection

---

# Verification Checklist

- SSH successfully enabled on Floor 1 Router
- SSH successfully enabled on Floor 2 Router
- SSH successfully enabled on Floor 3 Router
- RSA keys generated
- Local administrator account created
- Remote login tested successfully
- Switch Port Security enabled
- Sticky MAC Address learned
- Only one device permitted on secured port
- Port configured to shut down upon security violation

---

# Results

✅ SSH Remote Access Configured

✅ Local User Authentication Enabled

✅ RSA Encryption Keys Generated

✅ SSH Login Successfully Tested

✅ Switch Port Security Configured

✅ Sticky MAC Address Learning Enabled

✅ Unauthorized Device Protection Implemented

✅ Hotel Network Security Successfully Enhanced

---

# Conclusion

This lab demonstrates two essential network security technologies commonly used in enterprise environments. SSH provides secure, encrypted remote management of Cisco routers, replacing insecure management protocols such as Telnet. Switch Port Security strengthens access-layer security by allowing only authorized devices to connect through specific switch ports using Sticky MAC learning and violation protection. Combined with VLAN segmentation and OSPF routing, these configurations create a more secure and manageable hotel network infrastructure while following industry best practices for network administration.
