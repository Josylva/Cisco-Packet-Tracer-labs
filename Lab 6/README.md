# Office Inter-Department Routing Using a Cisco Router

## Overview

This project demonstrates how a router can be used to connect multiple departments within an organization, allowing devices in different networks to communicate with one another. The network is divided into two departments, Sales and Human Resources (HR), each operating on its own subnet.

The lab covers subnetting, router interface configuration, static IP addressing, default gateway configuration, and inter-network communication testing.

---

# Objectives

- Design a network with multiple departments
- Subnet a network into two separate subnets
- Configure router interfaces for inter-network communication
- Assign static IP addresses to end devices
- Configure default gateways
- Verify connectivity between departments using ICMP (Ping)

---

# Network Topology

<img width="698" height="431" alt="image" src="https://github.com/user-attachments/assets/19804450-baa5-4891-8810-ceec31e28b8c" />


## Departments

### Sales Department

- Ada PC
- Paul PC
- Sales Printer
- Sales Switch

### Human Resources (HR) Department

- Jane PC
- Mark PC
- HR Printer
- HR Switch

### Core Network Device

- Cisco 2911 Router

---

# Devices Used

| Device Type | Quantity |
|------------|----------|
| PC | 4 |
| Printer | 2 |
| Switch | 2 |
| Cisco 2911 Router | 1 |

---

# Physical Connections

## Sales Department

| Device | Switch Port |
|----------|----------|
| Ada PC | FastEthernet0/1 |
| Paul PC | FastEthernet0/2 |
| Sales Printer | FastEthernet0/3 |
| Router | GigabitEthernet0/0 |

---

## HR Department

| Device | Switch Port |
|----------|----------|
| Jane PC | FastEthernet0/1 |
| Mark PC | FastEthernet0/2 |
| HR Printer | FastEthernet0/3 |
| Router | GigabitEthernet0/1 |

---

# Network Addressing Plan

The network provided is:

```text
172.16.35.0
```

The organization requires:

```text
2 Subnets
```

---

# Subnetting Calculation

### Determine Number of Bits Required

```text
2^n = Number of Subnets
2^1 = 2
n = 1
```

Borrowing one bit from the host portion gives:

```text
Subnet Mask = 255.255.255.128
```

CIDR Notation:

```text
/25
```

---

# Subnet Details

## Sales Department Network

| Parameter | Value |
|------------|------------|
| Network Address | 172.16.35.0/25 |
| First Usable Address | 172.16.35.1 |
| Last Usable Address | 172.16.35.126 |
| Broadcast Address | 172.16.35.127 |
| Default Gateway | 172.16.35.1 |

---

## HR Department Network

| Parameter | Value |
|------------|------------|
| Network Address | 172.16.35.128/25 |
| First Usable Address | 172.16.35.129 |
| Last Usable Address | 172.16.35.254 |
| Broadcast Address | 172.16.35.255 |
| Default Gateway | 172.16.35.129 |

---

# Step 1 - Configure the Router

Open the router CLI.

When prompted:

```text
Would you like to enter the initial configuration dialog?
```

Type:

```text
no
```

---

# Step 2 - Enable Router Interfaces

Enter the following commands:

```bash
enable
configure terminal
interface range gigabitEthernet0/0-1
no shutdown
```

This activates both router interfaces.

---

# Step 3 - Configure Router IP Addresses

Configure the Sales Department interface:

```bash
interface gigabitEthernet0/0
ip address 172.16.35.1 255.255.255.128
no shutdown
```

Configure the HR Department interface:

```bash
interface gigabitEthernet0/1
ip address 172.16.35.129 255.255.255.128
no shutdown
```

Save the configuration:

```bash
do write
```

Expected output:

```text
Building configuration...
[OK]
```

---

# Router Configuration Summary

| Interface | IP Address | Subnet Mask | Department |
|------------|------------|------------|------------|
| GigabitEthernet0/0 | 172.16.35.1 | 255.255.255.128 | Sales |
| GigabitEthernet0/1 | 172.16.35.129 | 255.255.255.128 | HR |

---

# Step 4 - Configure Sales Department Devices

## Ada PC

| Setting | Value |
|----------|----------|
| IP Address | 172.16.35.2 |
| Subnet Mask | 255.255.255.128 |
| Default Gateway | 172.16.35.1 |

---
<img width="680" height="460" alt="image" src="https://github.com/user-attachments/assets/752ba800-2078-4207-b1f8-6d6900ab4d61" />

---

## Paul PC

| Setting | Value |
|----------|----------|
| IP Address | 172.16.35.3 |
| Subnet Mask | 255.255.255.128 |
| Default Gateway | 172.16.35.1 |

---

## Sales Printer

| Setting | Value |
|----------|----------|
| IP Address | 172.16.35.12 |
| Subnet Mask | 255.255.255.128 |
| Default Gateway | 172.16.35.1 |


---
<img width="680" height="460" alt="image" src="https://github.com/user-attachments/assets/ca400692-0a6c-4ecc-b535-10d498b297ad" />

---

# Step 5 - Configure HR Department Devices

## Jane PC

| Setting | Value |
|----------|----------|
| IP Address | 172.16.35.130 |
| Subnet Mask | 255.255.255.128 |
| Default Gateway | 172.16.35.129 |

---

## Mark PC

| Setting | Value |
|----------|----------|
| IP Address | 172.16.35.139 |
| Subnet Mask | 255.255.255.128 |
| Default Gateway | 172.16.35.129 |

---

## HR Printer

| Setting | Value |
|----------|----------|
| IP Address | 172.16.35.138 |
| Subnet Mask | 255.255.255.128 |
| Default Gateway | 172.16.35.129 |

---

# Step 6 - Verify Router Configuration

Use the following commands:

```bash
show ip interface brief
```

Expected result:

- GigabitEthernet0/0 should be UP
- GigabitEthernet0/1 should be UP

---

# Step 7 - Test Connectivity

From Ada's PC, open:

```text
Desktop → Command Prompt
```

Run:

```bash
ping 172.16.35.130
```

This sends an ICMP Echo Request to Jane's PC in the HR Department.

Expected output:

```text
Reply from 172.16.35.130

```
Successful replies confirm that the router is correctly routing traffic between both departments.

---
<img width="680" height="460" alt="image" src="https://github.com/user-attachments/assets/156075a6-7f60-4b8c-849f-519ebc845fe4" />

---
# Verification Checklist

- Sales devices can reach the Sales printer
- HR devices can reach the HR printer
- Router interfaces are operational
- Devices can communicate across subnets
- Default gateways are configured correctly
- Ping between departments is successful

---

# Results

✅ Network Successfully Subnetted

✅ Router Interfaces Configured

✅ Static IP Addresses Assigned

✅ Default Gateways Configured

✅ Inter-Department Routing Functional

✅ Cross-Subnet Communication Verified

---

# Conclusion

This lab demonstrates the implementation of basic routing between two departmental networks using a Cisco 2911 router. By subnetting the original network into two /25 networks and assigning each department its own gateway, devices in separate broadcast domains can communicate efficiently. This project provides practical experience with subnetting, router configuration, IP addressing, and inter-network communication which is a fundamental skills required in enterprise networking environments.
