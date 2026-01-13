# Industrial CPwE Network Infrastructure

[![GNS3](https://img.shields.io/badge/GNS3-Network%20Simulation-green)](https://www.gns3.com/)
[![Cisco IOS](https://img.shields.io/badge/Cisco-IOS-blue)](https://www.cisco.com/)
[![CPwE](https://img.shields.io/badge/Architecture-CPwE-orange)](https://www.cisco.com/)

A comprehensive network infrastructure simulation for manufacturing industries based on **Cisco Converged Plantwide Ethernet (CPwE)** architecture, implementing IT/OT network segmentation, advanced routing protocols, and security policies using GNS3.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Network Topology](#network-topology)
- [Key Features](#key-features)
- [Network Segmentation](#network-segmentation)
- [Technologies Used](#technologies-used)
- [Configuration Details](#configuration-details)
- [Security Implementation](#security-implementation)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Documentation](#documentation)

---

## 🎯 Overview

This project demonstrates a complete industrial network infrastructure design following Cisco's **Converged Plantwide Ethernet (CPwE)** reference architecture. The network is segmented into distinct zones to ensure secure communication between IT (Information Technology) and OT (Operational Technology) systems while maintaining operational efficiency.

### Project Objectives

- **IT/OT Convergence**: Seamless integration between office IT systems and production OT systems
- **Security-First Design**: Implementation of network segmentation, VLANs, and ACLs
- **Scalability**: Hierarchical network design supporting future expansion
- **High Availability**: Redundant paths and redundancy at the distribution layer
- **Best Practices**: Following Cisco CPwE guidelines and industrial network standards

---

## 🏗️ Architecture

The network is designed with a three-tier hierarchical architecture:

### **Core Layer**

- Central routing backbone connecting office and production networks
- High-speed Layer 3 routing between major network segments
- Devices: `OFFICE-CORE-ROUTER`, `PRODUCTION-CORE-ROUTER`

### **Distribution Layer**

- Aggregation point for access layer switches
- Policy enforcement and VLAN routing
- Devices:
  - Office: `OFFICE-DISTRIBUTION-ROUTER`, `OFFICE-DISTRIBUTION-SWITCH`
  - Production: `PRODUCTION-DISTRIBUTION-ROUTER`, `PRODUCTION-DISTRIBUTION-SWITCH-1/2/3`

### **Access Layer**

- End-user device connectivity
- VLAN assignment and port security
- Devices: Multiple access switches for various departments and production zones

---

## 🗺️ Network Topology

### Topology Diagrams

Complete visualization of the network infrastructure is available in the `diagrams/` folder:

- **[Network Design Topology](diagrams/Design%20-%20Network%20Infrastructure%20Topology.jpg)** - Initial network topology design
- **[Network Implementation Topology](diagrams/Implementation%20-%20Network%20Infrastructure%20Topology.png)** - Implementation topology in GNS3

### Network Segmentation

The network is divided into three main segments:

### 1️⃣ **Office Network** (IT Zone)

```
- IT Control Department
- Finance Department
- Management Department
- Marketing Department
```

### 2️⃣ **Production Network** (OT Zone)

```
- Production Control
- 11 Production Areas
```

### 3️⃣ **Server Room** (Data Center)

```
- Database Server (DB-SERVER)
- Manufacturing Execution System (MES-SERVER)
- Network Attached Storage (NAS-STORAGE)
```

---

## ✨ Key Features

### Network Design

- ✅ **Hierarchical Architecture**: Core-Distribution-Access model
- ✅ **VLAN Segmentation**: Logical separation of network traffic
- ✅ **Inter-VLAN Routing**: Router-on-a-stick and SVI configuration
- ✅ **IPv6 Ready**: Dual-stack implementation with IPv6 tunneling

### Security

- 🔒 **Access Control Lists (ACLs)**: Traffic filtering and security policies
- 🔒 **Network Segmentation**: IT/OT isolation
- 🔒 **DHCP Snooping**: Protection against rogue DHCP servers
- 🔒 **Port Security**: MAC address filtering

### Routing & Switching

- 🔄 **Static Routing**: For predictable traffic patterns
- 🔄 **Dynamic Routing**: OSPF for scalability
- 🔄 **STP**: Loop prevention with Rapid-PVST+

### Services

- 📡 **DHCP Server**: Automatic IP address assignment
- 📡 **DNS Integration**: Name resolution services
- 📡 **IPv6 Tunneling**: GRE tunnel for IPv6 connectivity

---

## 🔧 Network Segmentation

### Office VLANs

| VLAN ID | Name       | Network       | IPv6 Subnet       |
| ------- | ---------- | ------------- | ----------------- |
| VLAN 10 | IT Control | 10.10.10.0/26 | FD00:ACAD:10::/64 |
| VLAN 20 | Finance    | 10.10.20.0/26 | FD00:ACAD:20::/64 |
| VLAN 30 | Management | 10.10.30.0/26 | FD00:ACAD:30::/64 |
| VLAN 40 | Marketing  | 10.10.40.0/26 | FD00:ACAD:40::/64 |

### Production VLANs

| VLAN ID  | Name                         | Network        | IPv6 Subnet        |
| -------- | ---------------------------- | -------------- | ------------------ |
| VLAN 100 | Material Warehouse           | 10.20.100.0/27 | FD00:CCCC:100::/64 |
| VLAN 101 | Metal Fabrication            | 10.20.101.0/27 | FD00:CCCC:101::/64 |
| VLAN 102 | Welding & Metal Assembly     | 10.20.102.0/27 | FD00:CCCC:102::/64 |
| VLAN 103 | Surface Treatment            | 10.20.103.0/27 | FD00:CCCC:103::/64 |
| VLAN 104 | CNC Milling                  | 10.20.104.0/27 | FD00:CCCC:104::/64 |
| VLAN 105 | PCB Finishing & Testing      | 10.20.105.0/27 | FD00:CCCC:105::/64 |
| VLAN 106 | Main Assembly                | 10.20.106.0/27 | FD00:CCCC:106::/64 |
| VLAN 107 | Sealing & Cover Installation | 10.20.107.0/27 | FD00:CCCC:107::/64 |
| VLAN 108 | Painting & Final Testing     | 10.20.108.0/27 | FD00:CCCC:108::/64 |
| VLAN 109 | Quality Control & Testing    | 10.20.109.0/27 | FD00:CCCC:109::/64 |
| VLAN 110 | Packaging & Warehouse        | 10.20.110.0/27 | FD00:CCCC:110::/64 |

### Server VLANs

| VLAN ID | Name        | Network       | Description                           |
| ------- | ----------- | ------------- | ------------------------------------- |
| VLAN 90 | NAS Storage | 10.30.90.0/29 | NAS server and storage                |
| VLAN 91 | DB Server   | 10.30.91.0/29 | Database server for production data   |
| VLAN 92 | MES Server  | 10.30.92.0/29 | Manufacturing Execution System server |

---

## 🛠️ Technologies Used

### Hardware (Simulation)

- **Cisco IOS Routers**: 7200 Series
- **Cisco Catalyst Switches**: Layer 2 switches
- **Industrial Ethernet Switches**: For OT environment

### Software & Tools

- **GNS3**: Network simulation platform
- **Cisco IOS**: Version 15.9
- **VPCS**: Virtual PC Simulator for endpoints

### Protocols & Standards

- **Routing**: Static, OSPF
- **Switching**: VLANs, VTP, STP (RSTP/PVST+)
- **Services**: DHCP, DNS
- **Security**: ACLs, Port Security, DHCP Snooping
- **Tunneling**: GRE (IPv6 over IPv4)

---

## 📝 Configuration Details

### Router Configuration Highlights

**Core Routers**

- Inter-site routing between office and production
- Static and dynamic routing protocols
- IPv6 tunneling configuration
- Loopback interfaces for management

**Distribution Routers**

- Inter-VLAN routing (SVI)
- DHCP server configuration
- Access Control Lists (ACLs)
- Default gateway for access layer

### Switch Configuration Highlights

**Distribution Switches**

- VTP Server/Client configuration
- Trunk ports configuration (802.1Q)
- Layer 3 SVIs for VLAN routing
- Spanning Tree Protocol optimization

**Access Switches**

- VLAN assignment per port
- Access port configuration
- Port security (MAC filtering)
- DHCP client configuration

### Server Configuration (Simulated)

**DB-SERVER** (Database Server)

- Static IP configuration
- Database connectivity testing

**MES-SERVER** (Manufacturing Execution System)

- Production data integration
- Real-time monitoring interface

**NAS-STORAGE** (Network Storage)

- Centralized file storage
- Backup and recovery system

---

## 🔐 Security Implementation

### Access Control Lists (ACLs)

**Office to Production**

```
- Deny direct access from office VLANs to production VLANs
- Allow only authorized management traffic
- Allow server access through controlled channels
```

**Production to Office**

```
- Deny production network access to office resources
- Allow MES server communication to database
- Log unauthorized access attempts
```

### Port Security

- MAC address limitation per port
- Sticky MAC learning for known devices
- Violation action: shutdown/restrict

### Best Practices Implemented

- ✅ Principle of least privilege
- ✅ Network segmentation (IT/OT separation)
- ✅ Defense in depth strategy
- ✅ Regular security audits (via ACL logs)

---

## 🚀 Getting Started

### Prerequisites

1. **GNS3** (Version 2.2+)

   ```bash
   # Download from https://www.gns3.com/software/download
   ```

2. **Cisco IOS Images**

   - c7200 router image
   - Cisco switch IOS image (vIOS or IOU)

3. **VPCS** (included with GNS3)

### Installation Steps

1. **Clone repository**

   ```bash
   git clone https://github.com/AhmadSyafiNurroyyan/industrial-cpwe-network.git
   cd industrial-cpwe-network
   ```

2. **Import GNS3 Project**

   - Open GNS3
   - File → Import portable project
   - Select `gns3_project/Network Topology in the Automation Industry.gns3project`

3. **Load Configurations**

   - Configurations are already loaded in the project
   - If needed, load manually from `configs/` directory
   - Copy-paste configurations to respective devices

4. **Start the Network**
   - Click "Start All Nodes" in GNS3
   - Wait for all devices to boot
   - Verify connectivity with ping tests

### Verification Commands

```bash
# Verify VLAN configuration
show vlan brief

# Check routing table
show ip route

# Verify trunk ports
show interfaces trunk

# Test DHCP
show ip dhcp binding

# Check ACL
show access-lists

# Verify IPv6 tunnel
show ipv6 interface brief
```

---

## 📂 Project Structure

```
industrial-cpwe-network/
├── README.md                          # Project documentation
├── configs/                           # Device configurations
│   ├── office/                        # Office network configurations
│   │   ├── OFFICE-DISTRIBUTION-ROUTER.cfg
│   │   ├── OFFICE-DISTRIBUTION-SWITCH_configs_i3_startup-config.cfg
│   │   ├── ITCONTROL-ACCESS-SWITCH_configs_i1_startup-config.cfg
│   │   ├── FINANCE-ACCESS-SWITCH_configs_i2_startup-config.cfg
│   │   ├── MANAGEMENT-ACCESS-SWITCH_configs_i11_startup-config.cfg
│   │   └── MARKETING-ACCESS-SWITCH1_configs_i12_startup-config.cfg
│   ├── production/                    # Production network configurations
│   │   ├── PRODUCTION-DISTRIBUTION-ROUTER.cfg
│   │   ├── PRODUCTION-DISTRIBUTION-SWITCH-1_configs_i8_startup-config.cfg
│   │   ├── PRODUCTION-DISTRIBUTION-SWITCH-2_configs_i10_startup-config.cfg
│   │   ├── PRODUCTION-DISTRIBUTION-SWITCH-3_configs_i9_startup-config.cfg
│   │   ├── ACCESS-SWITCH_configs_i5_startup-config.cfg
│   │   ├── INDUSTRIAL-SWITCH*.cfg     # Multiple industrial switches
│   │   └── ...
│   └── server-room/                   # Server infrastructure
│       ├── OFFICE-CORE-ROUTER.cfg
│       ├── PRODUCTION-CORE-ROUTER.cfg
│       ├── SERVER-ACCESS-SWITCH_configs_i4_startup-config.cfg
│       ├── DB-SERVER_startup.vpc
│       ├── MES-SERVER_startup.vpc
│       └── NAS-STORAGE_startup.vpc
├── diagrams/                          # Network diagrams
├── doc/                               # Complete documentation
└── gns3_project/                      # GNS3 project files
    └── Network Topology in the Automation Industry.gns3project
```

---

## 📚 Documentation

### Complete Documentation

For a deeper understanding of network design and implementation, complete documentation is available:

- **[Full Network Design Documentation](doc/Full_Network_Design_Documentation.pdf)** - Comprehensive documentation covering:
  - Network requirements analysis
  - Detailed architecture design
  - Complete device configurations
  - Testing and troubleshooting
  - Implementation best practices

### Topology Diagrams

Network visual diagrams are available in the `diagrams/` folder:

- **Network Design Topology** - Initial conceptual design
- **Network Implementation Topology** - GNS3 implementation screenshot

### Configuration Files

All device configurations are stored in the `configs/` directory and organized by network zone:

- **Office Configurations**: Office network routers, switches, and access layer devices
- **Production Configurations**: Production network infrastructure and industrial switches
- **Server Room Configurations**: Core routers, server access switches, and server startup configurations

---

## 👤 Author

**Ahmad Syafi Nurroyyan**

- LinkedIn: https://www.linkedin.com/in/ahmad-syafi-nurroyyan-34ab81321/
- GitHub: [@AhmadSyafiNurroyyan](https://github.com/AhmadSyafiNurroyyan)
- Email: [ahmadsyafinurroyyan@gmail.com]

---

## 📄 License

This project is available for educational and portfolio purposes. Feel free to use it as a reference for your own network engineering projects.

---

## 🙏 Acknowledgments

- Cisco Systems for CPwE reference architecture
- GNS3 community for the excellent simulation platform
- Industrial network best practices and standards

---

## 📞 Contact

For questions, suggestions, or collaboration opportunities, feel free to reach out!

**⭐ If you find this project helpful, please consider giving it a star!**

---

_Last Updated: January 2026_
