# 🚀 Production Medium-Scale Enterprise Network Project

An advanced, security-hardened, and fully automated enterprise network architecture built on corporate infrastructure paradigms. The system segregates departments, manages structural access policies through advanced boundaries, automatically leases logical addresses, and provides secure network boundary translations for world-wide external internet connectivity.

---

## 🛠️ Implemented Architectural Features
1. **Multi-VLAN Segmentation (IEEE 802.1Q):** Isolated operational broadcast boundaries for **HR (VLAN 10)** and **Engineering (VLAN 20)**.
2. **Inter-VLAN Routing (Router-on-a-Stick):** High-speed logical sub-interface routing utilizing a Cisco ISR4331 Gateway.
3. **Automated Host Architecture (DHCP Server):** Dynamic logical address tracking pools per VLAN, built natively inside the core router.
4. **Layer 4 Extended Firewall (Access Control Lists):** Precision security policy preventing data requests from the Engineering network to the HR database while safely enabling HR-initiated loops.
5. **Network Address Translation (NAT Overload / PAT):** Dynamic mapping translating internal RFC 1918 addresses into a single global WAN public tier interface (`8.8.8.1`) for cloud connectivity.
6. **Production Version Control (Git Deployment):** Complete infrastructure increments tracked, committed, and locked upstream[cite: 1].

---

## 📊 IP Allocation Table

| Network Domain | VLAN ID | IP Subnet Range | Default Local Gateway | NAT Dynamic Role |
| :--- | :---: | :--- | :--- | :--- |
| **HR Department** | 10 | `192.168.10.0/24` | `192.168.10.1` | Inside Local Scope |
| **Engineering Dept** | 20 | `192.168.20.0/24` | `192.168.20.1` | Inside Local Scope |
| **Internet / WAN** | Native | `8.8.8.0/24` | `8.8.8.1` | Outside Global Boundary |

---

## 🔒 Security Policy Logic (Extended ACL)
```text
ip access-list extended SECURE_HR
 deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 echo
 permit ip any any