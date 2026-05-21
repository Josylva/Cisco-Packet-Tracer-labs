# SMTP Email Configuration Using Cisco Packet Tracer

## Overview

This project demonstrates how to configure and test an SMTP and POP3 email environment using Cisco Packet Tracer. The lab simulates a small office network where users communicate internally through an email server while receiving IP addresses automatically using DHCP.

### Objectives
- Configure a local network using a switch

- Assign IP addresses automatically using DHCP

- Configure SMTP and POP3 services

- Create email user accounts

- Configure email clients on multiple PCs
- Test email communication between users

---

# Network Topology


<img width="460" height="340" alt="image" src="https://github.com/user-attachments/assets/12d1c97a-7339-41af-a1ee-0ccb80dd7ffd" />


## Devices Used

- 3 Personal Computers
  
- 1 Switch

- 1 Server

- Copper Straight-Through Cable

## Connection Layout

| Device | Switch Port |
|---|---|
| Jane PC | FastEthernet0/1 |
| Paul PC | FastEthernet0/2 |
| Sammy PC | FastEthernet0/3 |
| Server | FastEthernet0/6 |

All devices were connected directly to the switch using Copper Straight-Through cables.

---

# Step 1 – Configure Server IP Address

Open the Server and assign a static IP address.

### Server Configuration

| Setting | Value |
|---|---|
| IP Address | 192.168.1.15 |
| Subnet Mask | Auto Generated |

The server will provide:

- DHCP Service

- Email Service (SMTP & POP3)

---

# Step 2 – Configure DHCP Service

Navigate to:

```text
Server → Services → DHCP
```

Turn DHCP **ON**.

Configure:

| Setting | Value |
|---|---|
| Service | ON |
| Start IP Address | 192.168.1.1 |
| Subnet Mask | Auto Generated |

Create DHCP allocation for client devices.

---

# Step 3 – Request DHCP Address

Open each PC.

Navigate to:

```text
Desktop → Command Prompt
```

Run:

```bash
ipconfig /renew
```

Assigned IP addresses:

| User | Assigned IP |
|---|---|
| Jane | 192.168.1.1 |
| Paul | 192.168.1.2 |
| Sammy | 192.168.1.3 |

Successful assignment confirms DHCP is functioning correctly.

---

# Step 4 – Configure Email Service (SMTP & POP3)

Navigate to:

```text
Server → Services → EMAIL
```

Enable:

- SMTP → ON
- POP3 → ON

Enter:

```text
Domain Name: terax.com
```

Create user accounts.

| Username | Password |
|---|---|
| jane | jane123 |
| paul | paul123 |
| sammy | sammy123 |

To add users:

1. Enter Username

2. Enter Password

3. Click **(+) Add**

4. Repeat for each user

The server will act as both:

- Outgoing Mail Server (SMTP)

- Incoming Mail Server (POP3)

---

# Step 5 – Configure Email Client on Each PC

Navigate to:

```text
Desktop → Email
```

Configure each user.

## Jane Configuration

| Field | Value |
|---|---|
| Name | Jane |
| Email Address | jane@terax.com |
| Incoming Mail Server | 192.168.1.15 |
| Outgoing Mail Server | 192.168.1.15 |
| Username | jane |
| Password | jane123 |

---

## Paul Configuration

| Field | Value |
|---|---|
| Name | Paul |
| Email Address | paul@terax.com |
| Incoming Mail Server | 192.168.1.15 |
| Outgoing Mail Server | 192.168.1.15 |
| Username | paul |
| Password | paul123 |

---

## Sammy Configuration

| Field | Value |
|---|---|
| Name | Sammy |
| Email Address | sammy@terax.com |
| Incoming Mail Server | 192.168.1.15 |
| Outgoing Mail Server | 192.168.1.15 |
| Username | sammy |
| Password | sammy123 |

> Note: The server IP (`192.168.1.15`) is used as both Incoming and Outgoing Mail Server.

---

# Step 6 – Test Email Communication

## Test 1 – Paul Sends Email to Sammy

Navigate to:

```text
Paul PC → Desktop → Email → Compose
```

Example:

### To

```text
sammy@terax.com
```

### Subject

```text
New Launch
```

### Message

```text
Hi Sammy,

The new TeraX launch preparation is progressing well.
Please review the latest update.

Regards,
Paul
```

Click **Send**.

---

## Test 2 – Sammy Receives and Sends Update Request

Navigate to:

```text
Sammy PC → Desktop → Email
```

Click:

```text
Receive
```

Confirm email is received.

Compose another email.

### To

```text
jane@terax.com
```

### Subject

```text
Update on New Launch
```

### Message

```text
Hi Jane,

Just checking in to see if there are any updates regarding the new launch.

Thanks,
Sammy
```

Click **Send**.

<img width="480" height="360" alt="image" src="https://github.com/user-attachments/assets/afd5de07-c969-41f6-85a3-52e15ef7d0c3" />


---

## Test 3 – Jane Replies to Sammy

Navigate to:

```text
Jane PC → Desktop → Email
```

Click:

```text
Receive
```

Open Sammy's email and select:

```text
Reply
```

Example reply:

```text
Hi Sammy,

Thanks for checking in.

The launch preparation is progressing as planned and I will share additional updates soon.

Regards,

Jane
```

Click **Send**.

<img width="430" height="349" alt="image" src="https://github.com/user-attachments/assets/512b7981-fe7b-4324-91e4-86a870280276" />


---

# Verification

Successful configuration is confirmed when:

- DHCP assigns IP addresses automatically

- SMTP sends email successfully

- POP3 receives email successfully

- Users can send and receive emails

## Final Result

- ✅ DHCP Configuration Successful
- ✅ SMTP Configuration Successful
- ✅ POP3 Configuration Successful
- ✅ Email Communication Verified

This project demonstrates how to deploy a basic internal email system using Cisco Packet Tracer with centralized DHCP and SMTP/POP3 services.
