# IoT Home Automation Lab Using Cisco Packet Tracer

## Overview

This project demonstrates the deployment of a simple Internet of Things (IoT) home automation network using Cisco Packet Tracer. The lab integrates wireless connectivity, DHCP services, IoT registration, and remote device management through an IoT-enabled server.

The objective is to connect multiple smart home devices to a wireless network and manage them remotely through a centralized IoT server.

---

# Objectives

- Configure a wireless access point for IoT connectivity
- Connect IoT devices to a wireless network
- Configure DHCP services for automatic IP assignment
- Register IoT devices with a central IoT server
- Enable remote monitoring and control of smart devices
- Manage IoT devices from a PC using the IoT Monitor application

---

# Network Topology

<img width="680" height="430" alt="image" src="https://github.com/user-attachments/assets/d5c0cc4a-bb85-4ac1-9b5e-cb24fdabebee" />

---

## Devices Used

- 1 Personal Computer (PC)
- 1 Switch
- 1 Wireless Access Point
- 1 Server
- 4 IoT Devices
  - Garage Door
  - Ceiling Fan
  - Appliance
  - Reading Lamp
- Copper Straight-Through Cables

---

# Physical Connections

The following devices were connected directly to the switch using Copper Straight-Through cables:

| Device | Connection |
|----------|----------|
| PC | Switch |
| Server | Switch |
| Wireless Access Point | Switch |

The IoT devices connect wirelessly through the Access Point.

---

# Step 1 - Configure the Wireless Access Point

Navigate to:

```text
Access Point → Config → Port 1
```

Configure the wireless network name (SSID):

```text
SSID: Homespot
```
<img width="690" height="360" alt="image" src="https://github.com/user-attachments/assets/770bfa44-c79e-4583-8c77-6c6539886242" />

---

This SSID will be used by all IoT devices to connect to the network.

---

# Step 2 - Connect IoT Devices to the Wireless Network

For each IoT device:

- Garage Door
- Ceiling Fan
- Appliance
- Reading Lamp

Navigate to:

```text
Config → Wireless0
```

Enter the following SSID:

```text
Homespot
```

After applying the configuration, each IoT device will connect wirelessly to the Access Point.

---

# Step 3 - Configure the Server

Assign a static IP address to the server.

| Setting | Value |
|----------|----------|
| IP Address | 192.168.1.25 |

The server will function as:

- DHCP Server
- IoT Registration Server
- IoT Management Platform

---

# Step 4 - Configure DHCP Service

Navigate to:

```text
Server → Services → DHCP
```

Enable DHCP and configure an address pool.

This allows devices on the network to automatically receive:

- IP Address
- Subnet Mask

---

# Step 5 - Obtain DHCP Addresses

For all connected devices, renew or reactivate DHCP.

The server will automatically assign IP addresses to:

- PC
- Access Point
- Garage Door
- Ceiling Fan
- Appliance
- Reading Lamp

This eliminates the need for manual IP configuration.

---

# Step 6 - Enable IoT Services

Navigate to:

```text
Server → Services → IoT
```

Ensure the IoT Service is:

```text
ON
```

This service allows smart devices to register and communicate with the server.

---

# Step 7 - Create an IoT User Account

Navigate to:

```text
Server → Desktop → IoT Monitor
```

Click:

```text
Login
```

The login attempt will fail because no account has been registered yet.

Enter the server IP address:

```text
192.168.1.25
```

You will then be prompted to create an account.

Select:

```text
Sign Up
```

Create the following account:

| Field | Value |
|----------|----------|
| Username | admin |
| Password | admin |

The IoT management account is now ready for use.

---

# Step 8 - Register IoT Devices

For each IoT device:

- Garage Door
- Ceiling Fan
- Appliance
- Reading Lamp

Navigate to:

```text
Config → Settings → IoT Server
```

Enable:

```text
Remote
```

Enter the following details:

| Setting | Value |
|----------|----------|
| Server Address | 192.168.1.25 |
| Username | admin |
| Password | admin |

Save the configuration.

---

<img width="690" height="380" alt="image" src="https://github.com/user-attachments/assets/a84f76d8-e94e-4e12-b0c3-94cc7b611ebc" />

---

Repeat for all IoT devices.

The devices are now registered with the IoT server and can be managed remotely.

---

<img width="690" height="380" alt="image" src="https://github.com/user-attachments/assets/029cf098-558b-49c1-8d11-75d1cdc7d216" />


---

# Step 9 - Monitor and Control Devices

On the PC, navigate to:

```text
Desktop → IoT Monitor
```

Login using:

| Field | Value |
|----------|----------|
| Username | admin |
| Password | admin |

After logging in, all registered IoT devices will be visible within the dashboard.

---

# Device Management

The IoT Monitor allows administrators to:

- Open and close the Garage Door
- Turn the Ceiling Fan on or off
- Control the Appliance remotely
- Switch the Reading Lamp on or off
- Monitor device status in real time

All actions are performed through the centralized IoT management interface.

---


<img width="527" height="248" alt="image" src="https://github.com/user-attachments/assets/e0882310-e736-4ea7-86b9-0e01cfa2614e" />

---

# Verification

Successful configuration is confirmed when:

- All IoT devices connect to the Homespot wireless network
- Devices receive IP addresses from DHCP
- The IoT Service is enabled on the server
- IoT devices successfully register with the server
- The IoT Monitor displays all connected devices
- Devices can be remotely controlled from the PC

---

# Results

✅ Wireless Access Point Configured

✅ IoT Devices Connected to Wireless Network

✅ DHCP Configuration Successful

✅ IoT Service Enabled

✅ Device Registration Successful

✅ Remote Device Management Operational

✅ Home Automation Network Successfully Implemented

---

# Conclusion

This lab demonstrates the fundamentals of IoT deployment and home automation using Cisco Packet Tracer. By combining wireless networking, DHCP, IoT services, and centralized device management, administrators can remotely monitor and control smart devices from a single interface. The project provides practical experience with technologies commonly used in modern smart homes and IoT-enabled environments.
