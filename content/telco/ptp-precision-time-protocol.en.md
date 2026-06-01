---
title: "PTP (Precision Time Protocol)"
description: "IEEE 1588 time synchronisation for telecom and RAN: grandmaster, boundary and transparent clocks, profiled deployments for fronthaul, backhaul, and 5G TDD coordination with sub-microsecond accuracy."
tags: ["telco", "ptp", "ieee-1588", "sync", "timing", "fronthaul", "5g", "tdd", "grandmaster", "transport"]
website: https://standards.ieee.org/ieee/1588/
---

**Precision Time Protocol (PTP)**, standardised as **IEEE 1588**, distributes a common **reference time** across packet networks so that distributed nodes share a clock with **sub-microsecond to nanosecond** accuracy — far beyond what **NTP** typically achieves over IP. PTP operates in a **master–slave hierarchy**: a **Grandmaster Clock (GM)** holds traceability to **GNSS** (GPS, Galileo, etc.) or a **Primary Reference Time Clock (PRTC)**; **Boundary Clocks (BC)** terminate and regenerate timing on hops; **Transparent Clocks (TC)** correct residence time in switches without terminating the protocol. Messages (**Sync**, **Follow_Up**, **Delay_Req/Resp**, optional **Announce**) implement a **delay request–response** mechanism to estimate path asymmetry and offset each **Ordinary Clock (OC)** slave relative to the grandmaster.

Telecom and mobile deployments use **profiled** subsets of IEEE 1588 for interoperability:

| **Profile** | **Typical use** |
| --- | --- |
| **ITU-T G.8275.1** | Full timing support from PRTC; often **phase** delivery in RAN/backhaul |
| **G.8275.2** | Partial timing support; packet networks without full on-path support |
| **IEEE 802.1AS (gPTP)** | Time-sensitive networking (TSN) in Ethernet LANs |
| **SMPTE / AES67** | Media and broadcast (related ecosystem) |

In **5G**, synchronisation underpins **TDD** operation (aligned uplink/downlink slots across cells), **carrier aggregation**, **CoMP**, and **O-RAN fronthaul** (strict phase requirements between **O-DU** and **O-RU**, often **Class C** or better depending on split and band). **SyncE (Synchronous Ethernet)** frequently **carries frequency** on physical layer while **PTP carries phase/time** — combined **SyncE + PTP** architectures are common in operator transport. **Holdover** oscillators (OCXO, rubidium) maintain stability when GNSS or upstream reference fails.

Design and operations focus on **asymmetry**, **packet loss**, **VLAN/QoS** marking for timing traffic, **BC/TC placement** in switches (especially **Cell Site Routers** and **fronthaul switches**), and **monitoring** (TE, packet delay variation) per **ITU-T G.827x** series. Misconfiguration is a leading cause of **interference**, **handover failures**, and **PRACH issues** in TDD networks — making PTP as critical as routing for RAN engineers.

## Additional Information

- [IEEE 1588 Standard](https://standards.ieee.org/ieee/1588/)
- [ITU-T Timing and synchronization (G.827x)](https://www.itu.int/rec/T-REC-G/en)
- [O-RAN Synchronization specifications](https://www.o-ran.org/specifications)
