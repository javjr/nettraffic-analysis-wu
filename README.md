# Network Traffic Analysis & SOC Lab Write-Ups

Welcome to my personal home-lab repository! This repository documents hands-on exercises focused on network traffic analysis, packet inspection (Wireshark), VLAN segmentation, and Linux hardening, built as part of my preparation for a SOC Analyst role.

## Lab Purpose

Understand how common network reconnaissance, anomalies, and attacks appear at the packet level.

Verify network segmentation and firewall policies across isolated VLANs.

Build practical, reproducible blue-team documentation and troubleshooting habits.

## Home-Lab Architecture

All experiments are conducted in a self-hosted virtualized environment:

* Host OS: Ubuntu Linux (Native Dual-Boot)

* Hypervisor: KVM (virbr0 for NAT internet access)

* Router / Firewall: MikroTik RouterOS (KVM) managing inter-VLAN routing and firewall filter rules

* Bridge: bridge-LAN

* Virtual Switch (ubuntu host): br-vlan, br-vlan01

* VLAN 10 (br-vln10): Kali Linux (Attacker / Testing Node) — `192.168.10[.]0/24`

* VLAN 20 (br-vln20): Alpine Linux (Target / Monitored Node) — `192.168.20[.]0/24`

```text
[ Internet ]
     │
  (virbr0 - NAT)
     │
[ Ubuntu Host (KVM) ]
     │
[ MikroTik RouterOS ] ── Firewall Filter & Inter-VLAN Routing
   ├── br-vlan
   │    └── VLAN 10 (br-vln10) ──> [ Kali Linux ] 192.168.10.253
   └── br-vlan01
        └── VLAN 20 (br-vln20) ──> [ Alpine Linux ] 192.168.20.2
```

## Write-Ups Index

| # | Directory | Topic / Scenario | Key Tools | Focus Area |
| :--- | :--- | :--- | :--- | :--- |
| 01 | [`01-analysis-sS`](./01-analysis-sS/) | VLAN-to-VLAN TCP SYN Scan & Firewall Drop Analysis | Nmap, Wireshark, MikroTik | Packet Inspection & Firewall Filtering |
| 02 | [`02-analysis-sS`](./02-analysis-sS/) | VLAN20 to VLAN10 TCP SYN Scan on open port without Firewall Drop Analysis | Nmap, Wireshark, MikroTik, netcat | Packet Inspection & anomaly vs normal traffic|
| 03 | [`03-analysis-http`](./03-analysis-http/) | VLAN20 to VLAN10 http request on port `8080` | python3, wget, Wireshark, MikroTik |traffic on http protocol & follow TCP stream|

> *More scenarios covering firewall logging, lateral movement detection, and Linux host hardening will be added continuously.*

## Core Toolset

* **Packet Capture & Analysis:** Wireshark

* **Traffic Generation & Testing:** nmap, Netcat, curl, dsniff, yersinia

* **Infrastructure & Defense:** MikroTik RouterOS, Linux iproute2, bridge-utils, iptables

> *Note: Several tools above are used during lab setup, standalone testing, or upcoming scenarios in this repository, and may not all appear in detail in every individual write-up.*

> **Disclaimer:** All traffic captures, scans, and simulations in this repository were performed strictly within an isolated local lab environment for educational and defensive learning purposes.