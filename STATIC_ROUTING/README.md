# Enterprise High-Availability Network 🌐

### Project Overview
Designed and implemented a redundant enterprise network infrastructure using a **Triangle Mesh Topology**. The project focuses on **Floating Static Routes** to ensure 99.9% uptime between HQ and Branch offices, utilizing administrative distance manipulation for automated failover and self-healing.

### 🛠️ Key Technologies & Skills
* 🛡️ **High Availability (HA):** Engineered a fully redundant triangle mesh to eliminate single points of failure across WAN links.
* 📡 **Floating Static Routes:** Implemented automated path failover by configuring backup routes with higher **Administrative Distance (AD 100)**.
* 📟 **Management Plane:** Configured **Loopback** interfaces on all routers to provide persistent, stable device identity.
* 🔢 **VLSM Subnetting:** Optimized IPv4 address space using **/30** masks for point-to-point WAN links and **/24** for LAN segments.

---

### 🗺️ Network Topology
The design connects three core sites (HQ, IT Branch, HR Branch) via dual-homed fiber links.

![Network Topology Diagram](./STATIC_ROUTING.png)

### 📝 Addressing & Routing Scheme
| Site Node | Role | Loopback ID | LAN Subnet |
| :--- | :--- | :--- | :--- |
| **HQ-Server** | Core Hub | `1.1.1.1/32` | `192.168.1.0/24` |
| **IT-Branch** | Branch Node | `2.2.2.2/32` | `192.168.2.0/24` |
| **HR-Branch** | Branch Node | `3.3.3.3/32` | `192.168.3.0/24` |

---

### ⚙️ Routing Logic & Configuration
To achieve deterministic failover, the following Administrative Distance (AD) values were applied:

| Route Type | Admin Distance (AD) | Function |
| :--- | :--- | :--- |
| **Primary Route** | **1** | Default active path when the interface is UP. |
| **Floating Route** | **100** | Backup path; injected into the routing table **only** when the primary fails. |

**Sample Configuration (HQ-Server):**
```bash
ip route 192.168.2.0 255.255.255.0 10.1.1.2     ! Primary
ip route 192.168.2.0 255.255.255.0 10.1.1.6 100 ! Backup
```

### ✅ Verification Results

**1. Normal Operation (Primary Path)**
Verified that the router prefers the Primary Route (`10.1.1.2`) with the default Administrative Distance (AD) of 1.
![Normal Routing Table](./IP_ROUTE_WITHOUT_AD.png)

**2. Simulated Failure Event**
Manually triggered a `shutdown` on the primary WAN interface. The console logs confirm the state change to DOWN.
![Interface Failure Logs](./STATIC_ROUTE_WITHOUT_AD.png)

**3. Failover Convergence (Backup Path)**
The router automatically installed the **Floating Static Route** (`10.1.1.6`) with AD 100, restoring connectivity via the redundant link.
![Failover Routing Table](./IP_ROUTE_WITH_AD.png)

**4. Static Route Verification**
Executed `show ip route static` to isolate the routing entries. This confirms that the backup route is the **only** active static path in the Routing Information Base (RIB).
![Static Route Command Output](./STATIC_ROUTE_WITH_AD.png)

---

### 📂 Project Files

* **[Download Packet Tracer File (.pkt)](./STATIC_ROUTING.pkt)**
