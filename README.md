# Infrastruktur Jaringan Industrial CPwE

[![GNS3](https://img.shields.io/badge/GNS3-Simulasi%20Jaringan-green)](https://www.gns3.com/)
[![Cisco IOS](https://img.shields.io/badge/Cisco-IOS-blue)](https://www.cisco.com/)
[![CPwE](https://img.shields.io/badge/Arsitektur-CPwE-orange)](https://www.cisco.com/)

Simulasi infrastruktur jaringan komprehensif untuk industri manufaktur berbasis arsitektur **Cisco Converged Plantwide Ethernet (CPwE)**, mengimplementasikan segmentasi jaringan IT/OT, protokol routing lanjutan, dan kebijakan keamanan menggunakan GNS3.

---

## 📋 Daftar Isi

- [Ikhtisar](#ikhtisar)
- [Arsitektur](#arsitektur)
- [Topologi Jaringan](#topologi-jaringan)
- [Fitur Utama](#fitur-utama)
- [Segmentasi Jaringan](#segmentasi-jaringan)
- [Teknologi yang Digunakan](#teknologi-yang-digunakan)
- [Detail Konfigurasi](#detail-konfigurasi)
- [Implementasi Keamanan](#implementasi-keamanan)
- [Memulai](#memulai)
- [Struktur Project](#struktur-project)
- [Dokumentasi](#dokumentasi)

---

## 🎯 Ikhtisar

Project ini mendemonstrasikan desain infrastruktur jaringan industrial lengkap mengikuti arsitektur referensi **Converged Plantwide Ethernet (CPwE)** dari Cisco. Jaringan tersegmentasi ke dalam zona-zona yang berbeda untuk memastikan komunikasi aman antara sistem IT (Information Technology) dan OT (Operational Technology) sambil mempertahankan efisiensi operasional.

### Tujuan Project

- **Konvergensi IT/OT**: Integrasi mulus antara sistem IT kantor dan sistem OT produksi
- **Desain Mengutamakan Keamanan**: Implementasi segmentasi jaringan, VLANs, dan ACLs
- **Skalabilitas**: Desain jaringan hierarki yang mendukung ekspansi di masa depan
- **Ketersediaan Tinggi**: Jalur redundan dan redundansi di lapisan distribusi
- **Best Practices**: Mengikuti pedoman Cisco CPwE dan standar jaringan industrial

---

## 🏗️ Arsitektur

Jaringan dirancang dengan arsitektur hierarki tiga tingkat:

### **Core Layer (Lapisan Inti)**

- Backbone routing pusat yang menghubungkan jaringan kantor dan produksi
- Routing Layer 3 berkecepatan tinggi antar segmen jaringan utama
- Perangkat: `OFFICE-CORE-ROUTER`, `PRODUCTION-CORE-ROUTER`

### **Distribution Layer (Lapisan Distribusi)**

- Titik agregasi untuk switch lapisan akses
- Penegakan kebijakan dan routing VLAN
- Perangkat:
  - Kantor: `OFFICE-DISTRIBUTION-ROUTER`, `OFFICE-DISTRIBUTION-SWITCH`
  - Produksi: `PRODUCTION-DISTRIBUTION-ROUTER`, `PRODUCTION-DISTRIBUTION-SWITCH-1/2/3`

### **Access Layer (Lapisan Akses)**

- Konektivitas perangkat end-user
- Penetapan VLAN dan keamanan port
- Perangkat: Beberapa access switch untuk berbagai departemen dan zona produksi

---

## 🗺️ Topologi Jaringan

Jaringan dibagi menjadi tiga segmen utama:

### 1️⃣ **Jaringan Kantor** (Zona IT)

```
- Departemen IT Control
- Departemen Finance
- Departemen Management
- Departemen Marketing
```

### 2️⃣ **Jaringan Produksi** (Zona OT)

```
- Industrial Control Systems
- Peralatan Manufaktur
- Integrasi SCADA/MES
- Akses Lini Produksi
```

### 3️⃣ **Ruang Server** (Data Center)

```
- Database Server (DB-SERVER)
- Manufacturing Execution System (MES-SERVER)
- Network Attached Storage (NAS-STORAGE)
```

---

## ✨ Fitur Utama

### Desain Jaringan

- ✅ **Arsitektur Hierarki**: Model Core-Distribution-Access
- ✅ **Segmentasi VLAN**: Pemisahan logis lalu lintas jaringan
- ✅ **Inter-VLAN Routing**: Konfigurasi Router-on-a-stick dan SVI
- ✅ **IPv6 Ready**: Implementasi dual-stack dengan tunneling IPv6

### Keamanan

- 🔒 **Access Control Lists (ACLs)**: Filter lalu lintas dan kebijakan keamanan
- 🔒 **Segmentasi Jaringan**: Isolasi IT/OT
- 🔒 **DHCP Snooping**: Perlindungan terhadap rogue DHCP server
- 🔒 **Port Security**: Filtering alamat MAC

### Routing & Switching

- 🔄 **Static Routing**: Untuk pola lalu lintas yang dapat diprediksi
- 🔄 **Dynamic Routing**: OSPF untuk skalabilitas
- 🔄 **VTP**: Manajemen VLAN di seluruh switch
- 🔄 **STP**: Pencegahan loop dengan Rapid-PVST+

### Layanan

- 📡 **DHCP Server**: Penetapan alamat IP otomatis
- 📡 **Integrasi DNS**: Layanan resolusi nama
- 📡 **IPv6 Tunneling**: Tunnel GRE untuk konektivitas IPv6

---

## 🔧 Segmentasi Jaringan

### VLAN Kantor

| VLAN ID | Nama       | Network       | Deskripsi                 |
| ------- | ---------- | ------------- | ------------------------- |
| VLAN 10 | IT Control | 10.10.10.0/26 | Workstation departemen IT |
| VLAN 20 | Finance    | 10.10.20.0/26 | Departemen Finance        |
| VLAN 30 | Management | 10.10.30.0/26 | Kantor Management         |
| VLAN 40 | Marketing  | 10.10.40.0/26 | Departemen Marketing      |

### VLAN Produksi

| VLAN ID  | Nama               | Network        | Deskripsi                      |
| -------- | ------------------ | -------------- | ------------------------------ |
| VLAN 100 | Production Control | 10.20.100.0/24 | Sistem kontrol manufaktur      |
| VLAN 110 | SCADA              | 10.20.110.0/24 | Sistem SCADA/HMI               |
| VLAN 120 | PLC Network        | 10.20.120.0/24 | Programmable Logic Controllers |
| VLAN 130 | Sensors            | 10.20.130.0/24 | Sensor industrial dan IoT      |

### VLAN Server

| VLAN ID  | Nama    | Network         | Deskripsi                    |
| -------- | ------- | --------------- | ---------------------------- |
| VLAN 200 | Servers | 10.100.200.0/24 | Server database dan aplikasi |
| VLAN 210 | Storage | 10.100.210.0/24 | Sistem NAS dan storage       |

---

## 🛠️ Teknologi yang Digunakan

### Hardware (Simulasi)

- **Cisco IOS Routers**: Seri 7200
- **Cisco Catalyst Switches**: Switch Layer 2 dan Layer 3
- **Industrial Ethernet Switches**: Untuk lingkungan OT

### Software & Tools

- **GNS3**: Platform simulasi jaringan
- **Cisco IOS**: Versi 15.x
- **VPCS**: Virtual PC Simulator untuk endpoint

### Protokol & Standar

- **Routing**: Static, OSPF, IPv6
- **Switching**: VLANs, VTP, STP (RSTP/PVST+)
- **Services**: DHCP, DNS, NTP
- **Security**: ACLs, Port Security, DHCP Snooping
- **Tunneling**: GRE (IPv6 over IPv4)

---

## 📝 Detail Konfigurasi

### Highlight Konfigurasi Router

**Core Routers**

- Routing antar-site antara kantor dan produksi
- Protokol routing statis dan dinamis
- Konfigurasi tunneling IPv6
- Interface loopback untuk manajemen

**Distribution Routers**

- Inter-VLAN routing (SVI)
- Konfigurasi DHCP server
- Access Control Lists (ACLs)
- Default gateway untuk lapisan akses

### Highlight Konfigurasi Switch

**Distribution Switches**

- Konfigurasi VTP Server/Client
- Konfigurasi trunk ports (802.1Q)
- Layer 3 SVIs untuk routing VLAN
- Optimasi Spanning Tree Protocol

**Access Switches**

- Penetapan VLAN per port
- Konfigurasi access port
- Port security (filtering MAC)
- Konfigurasi DHCP client

### Konfigurasi Server

**DB-SERVER** (Database Server)

- Konfigurasi IP statis
- Testing konektivitas database

**MES-SERVER** (Manufacturing Execution System)

- Integrasi data produksi
- Interface monitoring real-time

**NAS-STORAGE** (Network Storage)

- Penyimpanan file terpusat
- Sistem backup dan recovery

---

## 🔐 Implementasi Keamanan

### Access Control Lists (ACLs)

**Kantor ke Produksi**

```
- Tolak akses langsung dari VLAN kantor ke VLAN produksi
- Izinkan hanya lalu lintas manajemen yang terotorisasi
- Izinkan akses server melalui saluran terkontrol
```

**Produksi ke Kantor**

```
- Tolak akses jaringan produksi ke sumber daya kantor
- Izinkan komunikasi MES server ke database
- Log percobaan akses tidak terotorisasi
```

### Port Security

- Pembatasan alamat MAC per port
- Sticky MAC learning untuk perangkat yang dikenal
- Aksi pelanggaran: shutdown/restrict

### Best Practices yang Diimplementasikan

- ✅ Prinsip least privilege
- ✅ Segmentasi jaringan (pemisahan IT/OT)
- ✅ Strategi defense in depth
- ✅ Audit keamanan berkala (via log ACL)

---

## 🚀 Memulai

### Prasyarat

1. **GNS3** (Versi 2.2+)

   ```bash
   # Download dari https://www.gns3.com/software/download
   ```

2. **Cisco IOS Images**

   - Image router c7200
   - Image Cisco switch IOS (vIOS atau IOU)

3. **VPCS** (sudah termasuk dalam GNS3)

### Langkah Instalasi

1. **Clone repository**

   ```bash
   git clone https://github.com/AhmadSyafiNurroyyan/industrial-cpwe-network.git
   cd industrial-cpwe-network
   ```

2. **Import Project GNS3**

   - Buka GNS3
   - File → Import portable project
   - Pilih `gns3_project/Network Topology in the Automation Industry.gns3project`

3. **Load Konfigurasi**

   - Konfigurasi sudah ter-load dalam project
   - Jika diperlukan, load manual dari direktori `configs/`
   - Copy-paste konfigurasi ke perangkat masing-masing

4. **Jalankan Jaringan**
   - Klik "Start All Nodes" di GNS3
   - Tunggu semua perangkat booting
   - Verifikasi konektivitas dengan tes ping

### Perintah Verifikasi

```bash
# Verifikasi konfigurasi VLAN
show vlan brief

# Cek routing table
show ip route

# Verifikasi trunk ports
show interfaces trunk

# Test DHCP
show ip dhcp binding

# Cek ACL
show access-lists

# Verifikasi IPv6 tunnel
show ipv6 interface brief
```

---

## 📂 Struktur Project

```
industrial-cpwe-network/
├── README.md                          # Dokumentasi project
├── configs/                           # Konfigurasi perangkat
│   ├── office/                        # Konfigurasi jaringan kantor
│   │   ├── OFFICE-DISTRIBUTION-ROUTER.cfg
│   │   ├── OFFICE-DISTRIBUTION-SWITCH_configs_i3_startup-config.cfg
│   │   ├── ITCONTROL-ACCESS-SWITCH_configs_i1_startup-config.cfg
│   │   ├── FINANCE-ACCESS-SWITCH_configs_i2_startup-config.cfg
│   │   ├── MANAGEMENT-ACCESS-SWITCH_configs_i11_startup-config.cfg
│   │   └── MARKETING-ACCESS-SWITCH1_configs_i12_startup-config.cfg
│   ├── production/                    # Konfigurasi jaringan produksi
│   │   ├── PRODUCTION-DISTRIBUTION-ROUTER.cfg
│   │   ├── PRODUCTION-DISTRIBUTION-SWITCH-1_configs_i8_startup-config.cfg
│   │   ├── PRODUCTION-DISTRIBUTION-SWITCH-2_configs_i10_startup-config.cfg
│   │   ├── PRODUCTION-DISTRIBUTION-SWITCH-3_configs_i9_startup-config.cfg
│   │   ├── ACCESS-SWITCH_configs_i5_startup-config.cfg
│   │   ├── INDUSTRIAL-SWITCH*.cfg     # Beberapa industrial switch
│   │   └── ...
│   └── server-room/                   # Infrastruktur server
│       ├── OFFICE-CORE-ROUTER.cfg
│       ├── PRODUCTION-CORE-ROUTER.cfg
│       ├── SERVER-ACCESS-SWITCH_configs_i4_startup-config.cfg
│       ├── DB-SERVER_startup.vpc
│       ├── MES-SERVER_startup.vpc
│       └── NAS-STORAGE_startup.vpc
├── diagrams/                          # Diagram jaringan (akan ditambahkan)
├── doc/                               # Dokumentasi tambahan
└── gns3_project/                      # File project GNS3
    └── Network Topology in the Automation Industry.gns3project
```

---

## 📚 Dokumentasi

### File Konfigurasi

Semua konfigurasi perangkat tersimpan dalam direktori `configs/` dan terorganisir berdasarkan zona jaringan:

- **Konfigurasi Kantor**: Router jaringan kantor, switch, dan perangkat lapisan akses
- **Konfigurasi Produksi**: Infrastruktur jaringan produksi dan industrial switch
- **Konfigurasi Ruang Server**: Core router, server access switch, dan konfigurasi startup server

### Konvensi Penamaan

**Routers**: `<ZONE>-<LAYER>-ROUTER.cfg`

- Contoh: `OFFICE-DISTRIBUTION-ROUTER.cfg`

**Switches**: `<NAME>_configs_i<ID>_startup-config.cfg`

- Contoh: `ITCONTROL-ACCESS-SWITCH_configs_i1_startup-config.cfg`

**Servers**: `<NAME>_startup.vpc`

- Contoh: `DB-SERVER_startup.vpc`

---

## 🎓 Hasil Pembelajaran

Dengan mempelajari project ini, Anda akan mempelajari:

- ✅ **Arsitektur CPwE**: Prinsip desain jaringan industrial
- ✅ **Segmentasi Jaringan**: Strategi pemisahan IT/OT
- ✅ **Desain Hierarki**: Model Core-Distribution-Access
- ✅ **Konfigurasi VLAN**: Trunk ports, VTP, dan inter-VLAN routing
- ✅ **Protokol Routing**: Static routes, OSPF, dan IPv6 tunneling
- ✅ **Kebijakan Keamanan**: ACLs, port security, dan traffic filtering
- ✅ **Jaringan Industrial**: Integrasi SCADA, MES, dan jaringan produksi
- ✅ **Skill GNS3**: Simulasi dan testing jaringan

---

## 🔍 Pengembangan Masa Depan

- [ ] Menambahkan diagram topologi jaringan
- [ ] Implementasi kebijakan QoS untuk lalu lintas industrial
- [ ] Konfigurasi monitoring SNMP
- [ ] Menambahkan redundansi dengan HSRP/VRRP
- [ ] Implementasi dynamic routing (OSPF/EIGRP)
- [ ] Menambahkan konfigurasi firewall
- [ ] Integrasi jaringan wireless
- [ ] Script otomasi jaringan (Python/Ansible)

---

## 👤 Pembuat

**Ahmad Syafi Nurroyyan**

- Portfolio: [Website Portfolio Anda]
- LinkedIn: [Profil LinkedIn Anda]
- GitHub: [@AhmadSyafiNurroyyan](https://github.com/AhmadSyafiNurroyyan)
- Email: [Email Anda]

---

## 📄 Lisensi

Project ini tersedia untuk tujuan edukasi dan portfolio. Silakan gunakan sebagai referensi untuk project network engineering Anda sendiri.

---

## 🙏 Acknowledgments

- Cisco Systems untuk arsitektur referensi CPwE
- Komunitas GNS3 untuk platform simulasi yang excellent
- Best practices dan standar jaringan industrial

---

## 📞 Kontak

Untuk pertanyaan, saran, atau kesempatan kolaborasi, jangan ragu untuk menghubungi!

**⭐ Jika project ini bermanfaat, pertimbangkan untuk memberikan star!**

---

_Terakhir Diperbarui: Desember 2025_
