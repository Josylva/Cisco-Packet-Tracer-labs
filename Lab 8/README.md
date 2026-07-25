# 🏢 Multi-Floor Network Project

## 📖 Project Overview
This project designs a **three-floor enterprise network topology** using Cisco 2911 routers, 2960 switches, and access points. Each floor hosts multiple departments, each with its own VLAN, printer, PC, and sometimes IP phones. Wi-Fi access is provided via access points on every floor. Routers are interconnected via serial DCE cables with HWIC-2T modules.

---
<img width="640" height="334" alt="DCE connection" src="https://github.com/user-attachments/assets/078010aa-e5cb-4e34-aa35-ce0d422f0cb1" />

---
<img width="508" height="430" alt="Added Slot" src="https://github.com/user-attachments/assets/a5f0fe69-0b8d-481e-af8b-eedaafbf3005" />


## 🔧 Hardware Setup
- **Routers:** 3 × Cisco 2911 (one per floor)
- **Switches:** 3 × Cisco 2960-24TT (one per floor)
- **Modules:** HWIC-2T added to each router for serial connectivity
- **Connections:**
  - Routers connected via DCE cables (`Serial0/2/0`, `Serial0/2/1`)
  - Switches connected to routers via `GigabitEthernet0/0`
- **Access Points:** One per floor for Wi-Fi coverage
- **End Devices:** PCs, Printers, IP Phones, Smartphones, Tablets, Laptops

---
<img width="640" height="430" alt="Device arrangement" src="https://github.com/user-attachments/assets/3588f718-7dc2-48be-9e72-7b892d35f9a7" />
---

## 🖥️ Department & VLAN Layout

| Floor | Departments | VLAN | Network IP |
|-------|-------------|------|-------------|
| **1** | Reception, Restaurant | VLAN 10, VLAN 20 | 172.16.10.0/24, 172.16.20.0/24 |
| **2** | Finance, Logistics, Sales | VLAN 50, VLAN 30, VLAN 40 | 172.16.50.0/24, 172.16.30.0/24, 172.16.40.0/24 |
| **3** | HR, Admin, IT | VLAN 80, VLAN 70, VLAN 60 | 172.16.80.0/24, 172.16.70.0/24, 172.16.60.0/24 |

> Each department has **1 PC + 1 Printer**. Some departments also include IP Phones.

---

## 🔌 Router Serial IP Addressing (/30 Links)

| Link | Floor Routers | IP Addresses |
|------|---------------|--------------|
| F1 ↔ F2 | Serial0/2/0 & Serial0/2/1 | 10.1.12.2 / 10.1.12.1 |
| F1 ↔ F3 | Serial0/2/0 & Serial0/2/1 | 10.1.13.2 / 10.1.13.1 |
| F2 ↔ F3 | Serial0/2/0 & Serial0/2/1 | 10.1.23.1 / 10.1.23.2 |

---

## 🖧 Switch VLAN Configuration

### Floor 1 Switch
```bash
Switch(config)# interface range fa0/3, fa0/5
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config)# interface range fa0/6-8
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode trunk
Switch(config)# do write
```
### Floor 2 Switch
```bash
Switch(config)# interface range fa0/2-3, fa0/6
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 50
Switch(config)# interface range fa0/4, fa0/7
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 40
Switch(config)# interface range fa0/1, fa0/8
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 30
Switch(config)# interface fa0/9
Switch(config-if)# switchport mode trunk
Switch(config)# do write
```
### Floor 3 Switch

```bash
Switch(config)# interface range fa0/7-8
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 80
Switch(config)# interface range fa0/5-6
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 70
Switch(config)# interface range fa0/3-4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 60
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode trunk
Switch(config)# do write
```
## 🌐 Router IP Address Configuration

> Note: Each serial link uses a **/30 subnet**, which provides only **2 usable IP addresses** — one for each end of the point-to-point connection.

### Floor 1 Router
```bash
Router> enable
Router# configure terminal
Router(config)# interface se0/2/1
Router(config-if)# ip address 10.1.13.2 255.255.255.252
Router(config)# interface se0/2/0
Router(config-if)# ip address 10.1.12.2 255.255.255.252
Router(config)# do write
```
### Floor 2 Router
```bash
Router> enable
Router# configure terminal
Router(config)# interface se0/2/1
Router(config-if)# ip address 10.1.12.1 255.255.255.252
Router(config)# interface se0/2/0
Router(config-if)# ip address 10.1.23.1 255.255.255.252
Router(config)# do write
```
### Floor 3 Router
```bash
Router> enable
Router# configure terminal
Router(config)# interface se0/2/1
Router(config-if)# ip address 10.1.23.2 255.255.255.252
Router(config)# interface se0/2/0
Router(config-if)# ip address 10.1.13.1 255.255.255.252
Router(config)# do write
```
- All links comes up

<img width="940" height="464" alt="All Links Up" src="https://github.com/user-attachments/assets/11d8235d-359a-443e-a0f0-12ce646c09e0" />



## Inter-VLAN Routing & DHCP

### Floor 1 Router
```bash
Router(config)# interface gig0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 172.16.20.1 255.255.255.0
Router(config)# interface gig0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 172.16.10.1 255.255.255.0

! DHCP Pools
Router(config)# ip dhcp pool Restaurant
Router(dhcp-config)# network 172.16.20.0 255.255.255.0
Router(dhcp-config)# default-router 172.16.20.1
Router(dhcp-config)# dns-server 172.16.20.1
Router(config)# ip dhcp pool Reception
Router(dhcp-config)# network 172.16.10.0 255.255.255.0
Router(dhcp-config)# default-router 172.16.10.1
Router(dhcp-config)# dns-server 172.16.10.1
```
### Floor 2 Router
```bash
Router(config)# interface gig0/0.50
Router(config-subif)# encapsulation dot1Q 50
Router(config-subif)# ip address 172.16.50.1 255.255.255.0
Router(config)# interface gig0/0.40
Router(config-subif)# encapsulation dot1Q 40
Router(config-subif)# ip address 172.16.40.1 255.255.255.0
Router(config)# interface gig0/0.30
Router(config-subif)# encapsulation dot1Q 30
Router(config-subif)# ip address 172.16.30.1 255.255.255.0

! DHCP Pools
Router(config)# ip dhcp pool Finance
Router(dhcp-config)# network 172.16.50.0 255.255.255.0
Router(dhcp-config)# default-router 172.16.50.1
Router(dhcp-config)# dns-server 172.16.50.1
Router(config)# ip dhcp pool Sales
Router(dhcp-config)# network 172.16.40.0 255.255.255.0
Router(dhcp-config)# default-router 172.16.40.1
Router(dhcp-config)# dns-server 172.16.40.1
Router(config)# ip dhcp pool Logistics
Router(dhcp-config)# network 172.16.30.0 255.255.255.0
Router(dhcp-config)# default-router 172.16.30.1
Router(dhcp-config)# dns-server 172.16.30.1
```
### Floor 3
``` bash
Router(config)# interface gig0/0.80
Router(config-subif)# encapsulation dot1Q 80
Router(config-subif)# ip address 172.16.80.1 255.255.255.0
Router(config)# interface gig0/0.70
Router(config-subif)# encapsulation dot1Q 70
Router(config-subif)# ip address 172.16.70.1 255.255.255.0
Router(config)# interface gig0/0.60
Router(config-subif)# encapsulation dot1Q 60
Router(config-subif)# ip address 172.16.60.1 255.255.255.0

! DHCP Pools
Router(config)# ip dhcp pool HR
Router(dhcp-config)# network 172.16.80.0 255.255.255.0
Router(dhcp-config)# default-router 172.16.80.1
Router(dhcp-config)# dns-server 172.16.80.1
Router(config)# ip dhcp pool Admin
Router(dhcp-config)# network 172.16.70.0 255.255.255.0
Router(dhcp-config)# default-router 172.16.70.1
Router(dhcp-config)# dns-server 172.16.70.1
Router(config)# ip dhcp pool IT
Router(dhcp-config)# network 172.16.60.0 255.255.255.0
Router(dhcp-config)# default-router 172.16.60.1
Router(dhcp-config)# dns-server 172.16.60.1
```
- On each connected device, change the IP configuration to **DHCP**.  
<img width="513" height="487" alt="DHCP PC " src="https://github.com/user-attachments/assets/cb67a2b3-1669-46ab-abe8-a22cdc68c56f" />

- Use the **ping** command to verify connectivity by testing communication between systems located in different VLANs.
<img width="429" height="222" alt="ping in floor 3" src="https://github.com/user-attachments/assets/8c093a81-6b52-4898-bc58-bc2f8210114c" />

<img width="431" height="360" alt="PC0 Ping correct" src="https://github.com/user-attachments/assets/b4a55b44-d820-45dd-a555-76ac1b7e357a" />

## 📡 OSPF Configuration

### Floor 1 Router
```bash
Router(config)# router ospf 10
Router(config-router)# network 10.1.12.0 255.255.255.252 area 0
Router(config-router)# network 10.1.13.0 255.255.255.252 area 0
Router(config-router)# network 172.16.10.0 255.255.255.0 area 0
Router(config-router)# network 172.16.20.0 255.255.255.0 area 0
Router(config-router)# do write
```
### Floor 2
```bash
Router(config)# router ospf 10
Router(config-router)# network 10.1.12.0 255.255.255.252 area 0
Router(config-router)# network 10.1.23.0 255.255.255.252 area 0
Router(config-router)# network 172.16.30.0 255.255.255.0 area 0
Router(config-router)# network 172.16.40.0 255.255.255.0 area 0
Router(config-router)# network 172.16.50.0 255.255.255.0 area 0
Router(config-router)# do write
```
### Floor 3
```bash
Router(config)# router ospf 10
Router(config-router)# network 10.1.23.0 255.255.255.252 area 0
Router(config-router)# network 10.1.13.0 255.255.255.252 area 0
Router(config-router)# network 172.16.60.0 255.255.255.0 area 0
Router(config-router)# network 172.16.70.0 255.255.255.0 area 0
Router(config-router)# network 172.16.80.0 255.255.255.0 area 0
Router(config-router)# do write
```
<img width="404" height="130" alt="Router 1 OSPF" src="https://github.com/user-attachments/assets/d3caa3ab-e4a3-4f52-936c-074460862592" />


<img width="406" height="155" alt="Router 2 OSPF" src="https://github.com/user-attachments/assets/5bc57959-261d-4bfb-9465-6918cbc36d12" />


<img width="414" height="154" alt="F3 router OSPF" src="https://github.com/user-attachments/assets/79defb4b-5ff2-4094-8858-7ce67b37afb0" />

## Access Point Configuration
### Floor 1

SSID: floor1

Password: floor1@123

Devices: 1 Laptop, 1 Tablet, 1 Smartphone

Switch Port AP Setup:
``` bash
Switch(config)# interface FastEthernet0/4
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# do write
```

### Floor 2
SSID: floor2

Password: floor2@123

Devices: 1 Laptop, 3 Smartphones

Switch Port AP Setup:
```bash
Switch(config)# interface fa0/5
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 30
Switch(config-if)# do write
```
Floor 3
SSID: floor3

Password: floor3@123

Devices: 1 Laptop, 3 Smartphones

Switch Port AP Setup:
```bash
Switch(config)# interface fa0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 60
Switch(config-if)# do write
```
> note access point ports are Fastethernet0/4 for Floor 1 Fastethernet0/5 for Floor 2 and Fastethernet0/2 for Floor 3 enhance the configuration
<img width="959" height="437" alt="Wifi connection in Smart Hotel" src="https://github.com/user-attachments/assets/ac8c2fd1-142b-49bf-9f97-fe77796e5194" />

## SSH Configuration
### Floor 1 Router

```bash
Router(config)# hostname F1-Router
F1-Router(config)# ip domain-name stack
F1-Router(config)# username stack password stack
F1-Router(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
% Generating 1024 bit RSA keys...[OK]
F1-Router(config)# line vty 0 15
F1-Router(config-line)# login local
F1-Router(config-line)# transport input ssh
F1-Router(config-line)# do write
```
### Floor 2 Router
```bash
Router(config)# hostname F2-Router
F2-Router(config)# ip domain-name stack
F2-Router(config)# username stack password stack
F2-Router(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
% Generating 1024 bit RSA keys...[OK]
F2-Router(config)# line vty 0 15
F2-Router(config-line)# login local
F2-Router(config-line)# transport input ssh
F2-Router(config-line)# do write
```

### Floor 3 Router
``` bash
Router(config)# hostname F3-Router
F3-Router(config)# ip domain-name stack
F3-Router(config)# username stack password stack
F3-Router(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
% Generating 1024 bit RSA keys...[OK]
F3-Router(config)# line vty 0 15
F3-Router(config-line)# login local
F3-Router(config-line)# transport input ssh
F3-Router(config-line)# do write
```
## Verification:  
From any PC, open Command Prompt and run:
```bash
ssh -l stack 10.1.12.2
```
<img width="548" height="346" alt="ssh router 1" src="https://github.com/user-attachments/assets/05abbe45-35d1-4cba-a94a-21ce535399bf" />

## 🛡️ Switch Port Security (Floor 3 IT Department)
```bash
Switch(config)# interface fa0/4
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 1
Switch(config-if)# switchport port-security mac-address sticky
Switch(config-if)# switchport port-security violation shutdown
Switch(config-if)# do write
```
- This ensures only one device (the IT PC) can connect on port fa0/4.
- If another device connects, the port will go into err-disabled state.
- Test by replacing the IT PC with another device tries to connect, DHCP will fail and the port will shut down.

<img width="940" height="500" alt="New PC fails to connect" src="https://github.com/user-attachments/assets/7a7cfd1d-616a-45c3-957d-2260c7d09a48" />


<img width="371" height="120" alt="Violation mode PC1" src="https://github.com/user-attachments/assets/99ec8076-0475-47d8-82c0-d8519b375edd" />

> From the Switch log we can see the reason why the port fa0/4 is shutdown.

# Network Features Demonstrated

- Secure remote administration using SSH
- RSA public-key encryption
- VLAN-based departmental segmentation
- OSPF dynamic routing
- Switch Port Security
- Sticky MAC Address Learning

# Conclusion

This lab demonstrates essential network security technologies commonly used in enterprise environments. SSH provides secure, encrypted remote management of Cisco routers, replacing insecure management protocols such as Telnet. Switch Port Security strengthens access-layer security by allowing only authorized devices to connect through specific switch ports using Sticky MAC learning and violation protection. Combined with VLAN segmentation and OSPF routing, these configurations create a more secure and manageable hotel network infrastructure while following industry best practices for network administration.
