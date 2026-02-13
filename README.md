# 🌐 Routing Protocols in Computer Network

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco-Packet_Tracer-blue) ![Routing](https://img.shields.io/badge/Protocols-All-green)

A complete collection of Cisco routing protocol configurations and simulations. This project demonstrates how to configure, verify, and troubleshoot every major routing protocol used in modern networking.

---

## 🎯 Project Goal
To master the implementation of Interior (IGP) and Exterior (EGP) routing protocols using **Cisco IOS**.

---

## 📡 Protocols Included

| Protocol | Type | Usage |
| :--- | :--- | :--- |
| **Static** | Manual | Small Networks, Stub Networks & Default Routes |
| **RIPv2** | Distance Vector | Legacy & Small Networks |
| **EIGRP** | Hybrid | Cisco Enterprise Networks |
| **OSPF** | Link State | Industry Standard (Single & Multi-Area) |
| **IS-IS** | Link State | Service Provider Backbones |
| **BGP** | Path Vector | Internet Core & ISP Peering |

---

## 📂 Repository Structure
Each folder contains the **Packet Tracer (.pkt)** file and a text file with the **CLI Commands**.

```text
/
├── 01_Static_Routing/      # Default & Floating Static Routes
├── 02_RIPv2/               # Auto-summary disabled, Passive Interfaces
├── 03_EIGRP/               # Named Mode, K-Values, Feasible Successor
├── 04_OSPF/                # Process ID, Area Types (Stub/NSSA), LSA
├── 05_BGP/                 # eBGP vs iBGP, Neighbor Adjacency
└── topologies/             # Network Diagrams (Images)
