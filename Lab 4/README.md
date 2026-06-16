# DNS and HTTP Web Hosting Lab Using Cisco Packet Tracer

## Overview

This project demonstrates how DNS, DHCP, and HTTP services work together in a network environment. Users automatically receive IP addresses from a DHCP server, resolve domain names through a DNS server, and access hosted websites through web servers.

The lab simulates a simplified version of real-world web browsing where users can access websites using domain names instead of IP addresses.



---

# Objectives

- Configure a DHCP server for automatic IP assignment
- Configure a DNS server for name resolution
- Host websites on multiple web servers
- Create DNS A Records for domain mapping
- Verify successful web page access through domain names

---

# Network Topology

## Devices Used

- 3 Personal Computers
- 1 Switch
- 4 Servers
- Copper Straight-Through Cables

---

# Physical Connections

| Device | Switch Port |
|----------|----------|
| DNS Server | FastEthernet0/1 |
| DHCP Server | FastEthernet0/2 |
| Paul PC | FastEthernet0/3 |
| Mark PC | FastEthernet0/4 |
| Jane PC | FastEthernet0/5 |
| Yahoo Server | FastEthernet0/6 |
| Google Server | FastEthernet0/7 |

All devices were connected directly to the switch using Copper Straight-Through cables.

---

<img width="460" height="390" alt="image" src="https://github.com/user-attachments/assets/8d1e57c0-b93e-4686-9838-e8a2ae0ca368" />


# Step 1 - Configure Static IP Addresses

Assign the following static IP addresses to the servers.

| Device | IP Address |
|----------|----------|
| DNS Server | 192.168.1.5 |
| DHCP Server | 192.168.1.7 |
| Google Server | 192.168.1.8 |
| Yahoo Server | 192.168.1.9 |

---

# Step 2 - Configure DHCP Service

Navigate to:

```text
DHCP Server → Services → DHCP
```

Enable the DHCP service and configure an address pool for client devices.

### Important

Add the DNS Server IP address:

```text
192.168.1.5
```

to the DHCP configuration.

This ensures that all devices receiving IP addresses from DHCP will automatically use the DNS server for domain name resolution.

---

# Step 3 - Obtain Client IP Addresses

On each client PC:

```text
Desktop → Command Prompt
```

Run:

```bash
ipconfig /renew
```

The DHCP server assigns the following addresses:

| User | Assigned IP Address |
|--------|--------|
| Paul | 192.168.1.15 |
| Mark | 192.168.1.16 |
| Jane | 192.168.1.17 |

---

# Step 4 - Configure DNS Records

Navigate to:

```text
DNS Server → Services → DNS
```

Enable the DNS service and create the following A Records.

| Domain Name | IP Address |
|-------------|------------|
| www.google.com | 192.168.1.8 |
| www.yahoo.com | 192.168.1.9 |

These records allow users to access websites using domain names instead of IP addresses.


<img width="490" height="320" alt="image" src="https://github.com/user-attachments/assets/52531b74-95f6-41ef-be8e-92694597de42" />


---

# Step 5 - Configure the Google Web Server

Navigate to:

```text
Google Server → Services → HTTP
```

Ensure the HTTP service is turned **ON**.

---

## Edit index.html

Replace the default page with:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Google</title>
</head>
<body>
    <center>
        <h2 style="color:blue;">Welcome to Google</h2>
    </center>
    <hr>
    <p>Search the world's information, including webpages, images, videos and more.</p>
    <p>Quick Links:</p>
    <a href="search.html">Search Page</a><br>
    <a href="images.html">Images</a><br>
    <a href="about.html">About Google</a><br>
    <a href="contact.html">Contact</a>
</body>
</html>
```

---

## Edit images.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Google - Image Showcase</title>
</head>
<body>
    <center>
        <h2 style="color:blue;">Google Image Showcase</h2>
        <p>Welcome to Google Images. Explore and discover visuals that inspire.</p>
        <a href="cscoptlogo177x111.jpg">
            <img src="cscoptlogo177x111.jpg" alt="Cisco Logo" width="200" height="120"/>
        </a>
        <p>Click the image to view it full size.</p>
        <br>
        <a href="index.html">Back to Home</a>
    </center>
</body>
</html>
```

---

# Step 6 - Configure the Yahoo Web Server

Navigate to:

```text
Yahoo Server → Services → HTTP
```

Ensure the HTTP service is turned **ON**.

---

## Edit index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Yahoo</title>
</head>
<body>
    <center>
        <h2 style="color:purple;">Welcome to Yahoo</h2>
    </center>
    <hr>
    <p>Yahoo helps you stay connected to what matters most — news, mail, sports, and more.</p>
    <p><strong>Quick Links:</strong></p>
    <a href="news.html">Yahoo News</a><br>
    <a href="mail.html">Yahoo Mail</a><br>
    <a href="sports.html">Yahoo Sports</a><br>
    <a href="finance.html">Yahoo Finance</a><br>
    <br>
    <a href="index.html">Back to Home</a>
</body>
</html>
```

---

## Edit images.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Yahoo - Image Showcase</title>
</head>
<body>
    <center>
        <h2 style="color:purple;">Yahoo Image Showcase</h2>
        <p>Welcome to Yahoo Images.</p>
        <a href="cscoptlogo177x111.jpg">
            <img src="cscoptlogo177x111.jpg" alt="Cisco Logo" width="200" height="120"/>
        </a>
        <p>Click the image to view it full size.</p>
        <br>
        <a href="index.html">Back to Home</a>
    </center>
</body>
</html>
```

---

# Step 7 - Test DNS Resolution and Website Access

Open a web browser on any client PC:

- Paul
- Mark
- Jane

Navigate to:

```text
www.google.com
```

The Google homepage should load successfully.

Next navigate to:

```text
www.yahoo.com
```

The Yahoo homepage should load successfully.

---

# Verification

Successful configuration is confirmed when:

- DHCP automatically assigns IP addresses to clients.
- DNS resolves domain names correctly.
- Google website loads when browsing to www.google.com.
- Yahoo website loads when browsing to www.yahoo.com.
- Users access websites using domain names instead of IP addresses.

---

<img width="690" height="450" alt="image" src="https://github.com/user-attachments/assets/43c83d62-0343-453a-b121-a2b7968a6153" />

---

<img width="690" height="450" alt="image" src="https://github.com/user-attachments/assets/73187086-892a-4228-9187-901c9d77dee4" />

---

# Results

✅ Static IP Configuration Successful

✅ DHCP Configuration Successful

✅ DNS Configuration Successful

✅ Google Web Server Successfully Hosted

✅ Yahoo Web Server Successfully Hosted

✅ Domain Name Resolution Verified

✅ Website Access Verified

---

# Conclusion

This lab demonstrates the interaction between DHCP, DNS, and HTTP services within a network. By configuring a DNS server, users can access websites through familiar domain names rather than memorizing IP addresses. This project provides a practical understanding of how web browsing functions in real-world enterprise and internet environments.
