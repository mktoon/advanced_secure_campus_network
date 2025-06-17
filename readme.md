
# 🚀 Secure Redundant Branch Network Deployment with Cisco ASA, HSRP, and VLAN Segmentation

## 📘 Overview
This project implements a **highly available and securely segmented branch office network** for Martin Luther King University. It integrates **redundant multilayer switches (MLSWs)**, a **Cisco ASA firewall**, **VLAN-based segmentation**, **HSRP for gateway redundancy**, and **NAT for internet access**. The infrastructure is built for scalability, fault tolerance, and centralized internet security via the firewall.

------------------------------------------------------------

## 🏗️ Network Architecture

- **Two Layer-3 Multilayer Switches (BR-MLS1 & BR-MLS2)**  
- Configured with **VLAN interfaces (SVIs)** for LAN segmentation  
- HSRP configured per VLAN to ensure **gateway redundancy**  
- Connected via trunk ports and Port-Channel for high availability  
- **Cisco ASA Firewall (Outside Gateway)**  
- Acts as perimeter security and NAT gateway  
- Redundant uplinks from both MLSWs  
- **VLANs Implemented**:
- `VLAN 20` – BR-WLAN  
- `VLAN 60` – BR-LAN (172.17.0.0/16)  
- `VLAN 90` – WLAN (10.11.0.0/16)  
- `VLAN 199` – Backhole (192.168.199.0/24)  
- **Routing** handled by MLSWs using static routes and HSRP
- **NAT and Internet Access** configured on the ASA

------------------------------------------------------------

## 📁 Features

- ✅ **High Availability**: HSRP provides failover between BR-MLS1 and BR-MLS2  
- 🔒 **Secure Perimeter**: Cisco ASA NATs internal subnets and filters traffic  
- 🧱 **Logical Segmentation**: VLANs isolate traffic for security and performance  
- 🔁 **Redundant Links**: Port-channels and trunked uplinks to ASA  
- 🧪 **Verification**: Connectivity, failover, NAT, and route tracking tested

------------------------------------------------------------

## ⚙️ Configuration Highlights

### ASA Firewall (NAT Configuration)
```
object network INSIDE1-OUTSIDE
 subnet 172.17.0.0 255.255.0.0
 nat (INSIDE1,OUTSIDE) dynamic interface

object network INSIDE1a-OUTSIDE
 subnet 172.17.0.0 255.255.0.0
 nat (INSIDE2,OUTSIDE) dynamic interface

object network INSIDE2-OUTSIDE
 subnet 10.11.0.0 255.255.0.0
 nat (INSIDE1,OUTSIDE) dynamic interface

object network INSIDE2a-OUTSIDE
 subnet 10.11.0.0 255.255.0.0
 nat (INSIDE2,OUTSIDE) dynamic interface
````

### MLSW VLAN + HSRP Configuration Example (BR-MLS1)

```
interface Vlan60
 description BR-LAN
 ip address 172.17.0.2 255.255.0.0
 standby 60 ip 172.17.0.1
 standby 60 priority 110
 standby 60 preempt

interface Vlan90
 description WLAN
 ip address 10.11.0.2 255.255.0.0
 standby 90 ip 10.11.0.1
 standby 90 priority 110
 standby 90 preempt
```

------------------------------------------------------------

## 🔍 Verification Commands

### On MLSW:
```
show standby brief
show ip route
ping <virtual IP>
```
### On ASA:
```
show nat
show route
```
------------------------------------------------------------
## 📦 Technologies Used

* Cisco Catalyst 3560/3750 Series (MLSW)
* Cisco ASA 5505/5506-X Series
* VLANs, HSRP, 802.1Q trunking, Port-Channel
* DHCP (or static addressing)
* NAT (PAT to OUTSIDE)
* Cisco Packet Tracer for simulation
------------------------------------------------------------
## 📝 Author
Micah Too
🔗 [GitHub](https://github.com/mktoon) • 
💼 [LinkedIn](https://linkedin.com/in/micah-too-baa51517b)
Cloud & Network Infrastructure Engineer

------------------------------------------------------------
