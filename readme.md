# 🚀 Secure Multi-Campus Network Design with Cisco ASA, VLANs, VPN, and HSRP

## 🏛️ About the Project

This is part of **Advanced Enterprise Networking Project #12**, focused on designing and deploying a **highly secure and redundant network** for **A University**, which spans **two geographically separate campuses**.

The infrastructure is built to serve **30,000+ users**, accommodate scalability for future growth, and ensure secure access to central resources, cloud services, and wireless connectivity across faculties.

----------------------------------------------------------------------------------

## 📘 Project Overview

The project meets the following goals:

- 🔐 Secure user access via ASA firewalls and VLAN segmentation
- 🔁 High availability using HSRP on multilayer switches
- 🌐 Secure inter-campus communication via **Site-to-Site IPsec VPN**
- 📡 Wireless LAN coverage via WLC and LAPs per department
- ☁️ Access to cloud-hosted services (Google Cloud)
- ⚙️ Centralized DHCP, DNS, FTP, and SMTP servers in a secure DMZ

----------------------------------------------------------------------------------

## 🏗️ Network Architecture

### 🧩 Main Campus

- **Core Switches (MLSWs)**: VLAN interfaces for routing
- **Cisco ASA 5500 Firewall**: NAT + DMZ segmentation
- **WLC + LAPs**: Wireless access for students, staff, guests
- **Server Farm (DMZ)**: Static IPs for DNS, DHCP, Web, FTP, SMTP, etc.
- **Routing Protocol**: OSPF across all Layer 3 devices
- **Management VLAN (10)**: `172.16.10.0/24`
- **LAN VLAN (20)**: `192.168.0.0/16`
- **WLAN VLAN (50)**: `10.10.0.0/16`
- **DMZ VLAN (30)**: `10.20.20.0/27`
- **Blackhole VLAN (199)**: Unused ports

### 🛰️ Branch Campus

- **Dual MLSWs with HSRP for redundancy**
- **Cisco ASA firewall** connecting to main campus via VPN
- **VLANs and subnetting** similar to the main campus
- **NAT for local internet access**
- **DHCP relay to main campus servers**

----------------------------------------------------------------------------------

## 🔐 Security Features

- 🔐 **Cisco ASA firewalls** on both campuses with inspection policies
- 🧱 VLAN-based traffic isolation for LAN, WLAN, DMZ, and management
- 🌐 **Site-to-Site IPsec VPN** connecting campuses
- 🔁 HSRP ensures **default gateway failover**
- 📶 Wireless devices authenticated and segmented by VLAN
- 🚫 Blackhole VLAN to prevent rogue connections
- 🔒 Standard ACL allows SSH only from the admin PC

----------------------------------------------------------------------------------

## 📡 Wireless Deployment

- **WLC** deployed at the main campus
- **Lightweight APs** per department (centrally managed)
- SSIDs: `CampusWiFi`, `GuestWiFi`
- VLAN 50 assigned for WLAN
- DHCP relay enabled

----------------------------------------------------------------------------------

## ⚙️ Configuration Highlights

### 🔧 HSRP on Core Switch (Main Campus)

```bash
interface Vlan10
 ip address 172.16.10.2 255.255.255.0
 standby 10 ip 172.16.10.1
 standby 10 priority 110
 standby 10 preempt
```

### 🔧 ASA NAT Example (Main Campus)

```bash
object network INSIDE_LAN
 subnet 192.168.0.0 255.255.0.0
 nat (inside,outside) dynamic interface

route outside 0.0.0.0 0.0.0.0 105.100.50.1
```

### 🔧 OSPF Configuration

```bash
router ospf 1
 network 192.168.0.0 0.0.255.255 area 0
 network 10.10.0.0 0.0.255.255 area 0
 network 172.16.10.0 0.0.0.255 area 0
```

---

## 🧪 Testing & Validation

- ✅ Inter-VLAN communication working on all clients
- ✅ Internet access via ASA NAT
- ✅ VPN tunnel: branch ↔ main connectivity
- ✅ DHCP: devices auto-assigned correct IPs
- ✅ HSRP: switch failover test passes
- ✅ Wireless client joins SSID and browses internal web
- ✅ ACL blocks SSH from unauthorized devices

----------------------------------------------------------------------------------

## 📦 Technologies Used

- Cisco Catalyst 2960/3850
- Cisco ASA 5506-X
- Wireless LAN Controller (WLC) & LAPs
- VLANs, HSRP, OSPF, Port-Channel, DHCP, NAT, ACL
- Cisco Packet Tracer (Simulation)

----------------------------------------------------------------------------------

## 📁 File Structure

```bash
📦secure-campus-network
    ┣ 📂configs
    ┃ ┣ main-campus-core1.txt
    ┃ ┣ branch-campus-asa.txt
    ┣ 📂diagrams
    ┃ ┗ ASCI.png
    ┃ ┗ highlevel.png
    ┣ 📂notes
    ┃ ┗ Network_Design_Diagram.pptx
    ┣ Advances Campus Network.pkt
    ┣ README.md

```

----------------------------------------------------------------------------------

## 👤 Author

**Micah Too**  
- [GitHub](https://github.com/mktoon) 
- [LinkedIn](https://linkedin.com/in/micah-too-baa51517b)

---