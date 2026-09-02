## 🌟 Overview

This project presents the design and implementation of a **Secure Enterprise Network Infrastructure** using Cisco Packet Tracer.

The objective is to design a realistic enterprise network that provides secure, reliable, scalable, and organized communication between different departments, network services, servers, and external networks.

The infrastructure combines Layer 2 switching, Layer 3 routing, VLAN segmentation, dynamic routing, network services, security mechanisms, and Internet connectivity.

This project was developed as a practical networking laboratory to apply and strengthen skills in:

- 🌐 Enterprise Network Architecture
- 🔀 Routing & Switching
- 🏷️ VLAN Segmentation
- 🔗 802.1Q Trunking
- 🧭 OSPF Dynamic Routing
- 🔐 Network Security (ACL, SSH, Port Security)
- 🖥️ DHCP & DNS Services
- 🌍 NAT/PAT & Internet Connectivity
- 🧪 Network Troubleshooting

## 🎯 Project Objectives

The main objectives of this project are to build an enterprise network capable of providing:

- Network segmentation using VLANs
- Inter-VLAN communication through Layer 3 routing
- Dynamic route exchange using OSPF
- Automatic IP configuration using DHCP
- Name resolution using DNS
- Controlled communication using security policies (ACL)
- Secure device administration via SSH
- Internet connectivity for internal users via NAT/PAT
- Scalable network architecture suitable for an enterprise environment

## 🏗️ Network Architecture

The enterprise network is organized into several functional components:

```
                           ☁️ INTERNET (simulated)
                                  │
                                  │
                           🌐 R-EDGE (Edge Router)
                                  │  NAT/PAT, default route
                                  │
                           🧭 R-CORE (Core Router)
                                  │  OSPF Area 0
                    ┌─────────────┴─────────────┐
                    │                           │
              🌐 R-BRANCH                 🔀 SW-CORE (Layer 3)
              (remote site)               SVIs, inter-VLAN routing
                                                 │
                              ┌──────────────────┼──────────────────┐
                              │                  │                  │
                         🔌 ACCESS SW       🔌 ACCESS SW       🔌 ACCESS SW
                         (DIR, RH, FIN...)  (SERVERS)          (GUEST)
                              │                  │                  │
                         💻 USERS           🖥️ DNS/WEB/FTP     💻 GUEST USERS
```

### 🔹 Core Layer
A Layer 3 switch (SW-CORE) provides high-speed inter-VLAN routing and participates in OSPF dynamic routing — chosen over router-on-a-stick to reflect a realistic enterprise design.

### 🔹 Access Layer
Access switches provide connectivity to end devices such as desktop computers and laptops, organized by department (Direction, HR, Finance, IT, Marketing, Support) and by function (Servers, Guest).

### 🔹 Server Network
The server infrastructure hosts essential enterprise services: DNS, HTTP, and FTP, isolated in a dedicated VLAN (Servers).

### 🔹 Guest Network
A dedicated Guest VLAN is fully isolated from internal resources via ACL, while retaining Internet access through NAT.

### 🔹 WAN / Internet
The edge router (R-EDGE) provides connectivity between the enterprise infrastructure and the external network, and a branch router (R-BRANCH) simulates a remote site connected via WAN.

## 🔀 Routing & Switching Architecture

The network combines Layer 2 and Layer 3 technologies to provide efficient communication.

**Layer 2 Technologies**
- VLANs
- 802.1Q Trunking

**Layer 3 Technologies**
- Inter-VLAN Routing (SVIs on a Layer 3 switch)
- OSPF
- Default routing toward the external network
- NAT/PAT (overload)

This architecture allows the network to remain organized while providing controlled communication between different departments and services.

## 🏷️ VLAN Segmentation

VLANs are used to logically separate users, services, and network infrastructure.

The purpose of VLAN segmentation is to:
- Reduce broadcast domains
- Improve network performance
- Increase security
- Isolate departments
- Simplify network administration
- Facilitate troubleshooting

| VLAN ID | Name | Network | Gateway (SVI) |
|---|---|---|---|
| 10 | DIRECTION | 172.16.10.0/24 | 172.16.10.1 |
| 20 | HR | 172.16.20.0/24 | 172.16.20.1 |
| 30 | FINANCE | 172.16.30.0/24 | 172.16.30.1 |
| 40 | IT | 172.16.40.0/24 | 172.16.40.1 |
| 50 | MARKETING | 172.16.50.0/24 | 172.16.50.1 |
| 60 | SUPPORT | 172.16.60.0/24 | 172.16.60.1 |
| 70 | SERVERS | 172.16.70.0/24 | 172.16.70.1 |
| 80 | GUEST | 172.16.80.0/24 | 172.16.80.1 |
| 99 | MGMT | 172.16.99.0/24 | 172.16.99.1 |

Each VLAN represents a specific logical network segment, while routing between VLANs is performed by the Layer 3 core switch.

## 🧭 OSPF Dynamic Routing

OSPF (Open Shortest Path First) is used as the dynamic routing protocol within the enterprise infrastructure, running in a single **Area 0**.

OSPF allows routers and the Layer 3 switch to dynamically exchange network information and calculate the best available paths.

**OSPF provides:**
- Dynamic route learning
- Automatic path calculation
- Fast convergence
- Adaptation to network topology changes

**Verification commands:**
```
show ip ospf neighbor
show ip route ospf
show ip protocols
```

A correctly established OSPF adjacency reaches the **FULL** state — confirmed between R-EDGE, R-CORE, R-BRANCH, and SW-CORE.

## 🖥️ Network Services

The enterprise infrastructure supports essential network services.

**DHCP**
DHCP automatically provides network configuration to clients, including IP address, subnet mask, default gateway, and DNS server — with a dedicated pool per user VLAN.

Verification from a client:
```
ipconfig /all
```

**DNS**
DNS provides hostname-to-IP address resolution for internal services.

**Web / FTP**
An internal Web server and an authenticated FTP server are hosted in the Servers VLAN.

These services simplify network administration and improve the user experience.

## 🛡️ Network Security

Security is integrated into the network architecture through segmentation and controlled communication.

Security mechanisms implemented in the project include:
- VLAN isolation
- ACL-based traffic filtering (complete isolation of the Guest VLAN)
- Secure device administration via **SSH v2** (RSA keys, Telnet disabled)
- **Port Security** (sticky MAC addresses, restrict violation mode)

The objective is to limit unauthorized access and protect critical enterprise resources.

## 🧪 Testing & Validation

The network was tested after configuration to verify the operation of its main components.

**VLAN Verification**
```
show vlan brief
```

**Trunk Verification**
```
show interfaces trunk
```

**OSPF Verification**
```
show ip ospf neighbor
show ip route ospf
```

**Inter-VLAN Connectivity**
```
ping <destination-ip>
```

**DHCP Verification**
```
ipconfig /all
```

**DNS Verification**
```
ping <hostname>
```

**Server Connectivity**
```
ping <server-ip>
```

**ACL / Guest Isolation Verification**
```
ping <internal-vlan-ip>
show access-lists
```

**NAT/PAT Verification**
```
show ip nat translations
```

Successful results confirm the correct operation of the major network components.




**📄 Packet Tracer Project**
The `.pkt` file contains the complete simulated network topology and device configurations.

**🖼️ Network Topology**
The `topology.png` file provides a visual overview of the enterprise network architecture.

## 💻 Software

Cisco Packet Tracer

The complete infrastructure was designed, configured, tested, and validated in a Cisco Packet Tracer simulation environment.

## 👩‍💻 Author

**Oumayma Selmi**
Telecommunications Engineer | Cybersecurity & Network Engineering

**Areas of Interest**
- Enterprise Networking
- Cisco Technologies
- Network Security
- Cybersecurity
- Cloud & DevSecOps

## ⭐ Project Summary

This project demonstrates the practical implementation of a secure, scalable, and reliable enterprise network, combining routing, switching, VLAN segmentation, dynamic routing, network services, and security in a single integrated infrastructure.

Designed and implemented by Oumayma Selmi.
