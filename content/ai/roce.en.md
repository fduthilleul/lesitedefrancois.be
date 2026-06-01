---
title: "RoCE (RDMA over Converged Ethernet)"
description: "RDMA on lossless Ethernet—an alternative to InfiniBand for GPU collective traffic and storage, widely deployed when AI clusters share a converged datacenter fabric."
tags: ["ai", "roce", "rdma", "ethernet", "networking", "nccl", "distributed-training"]
website: https://docs.nvidia.com/networking/display/MLNXv4/RDMA+over+Converged+Ethernet+(RoCE)
---

**RoCE (RDMA over Converged Ethernet)** implements **RDMA** semantics on **Ethernet** (RoCEv2 uses UDP/IP), so NICs can perform remote memory access with low **CPU** utilization over the same physical switches many enterprises already operate. Its objective is to deliver InfiniBand-like **GPU** communication economics—fast **NCCL** all-reduces, **NVMe-oF**, **llm-d** KV moves—without maintaining a separate InfiniBand fabric. RoCE requires **lossless Ethernet** behavior: Priority Flow Control (**PFC**), Explicit Congestion Notification (**ECN**), buffer tuning, and often dedicated traffic classes so RDMA traffic is not dropped under burst load.

Architecturally, RoCEv2 is routable L3 Ethernet; **InfiniBand** uses different link and subnet management. Misconfigured switches cause silent performance cliffs (retransmits, collapse to slow paths), so RoCE is as much a **datacenter design** choice as a NIC feature. Within a server, **NVLink** still handles GPU peer traffic; RoCE links **nodes**. The **CPU** role matches other RDMA: setup and orchestration, not per-byte copying. AI workloads do not distinguish RoCE vs IB at the **PyTorch** API—**NCCL** selects transports based on environment and hardware—but ops teams must qualify firmware, cable, and QoS end to end.

**Red Hat** documents RoCE on **RHEL** (ConnectX drivers, `rdma-core`, tuning guides) and **OpenShift** networking for accelerated workloads, overlapping telco core and AI cluster designs. Customers who standardize on Ethernet for cost and operations use RoCE for GPU scale-out while running **OpenShift AI** or bare-metal **training** clusters on supported RHEL. Red Hat support focuses on kernel, driver, and platform integration; switch QoS profiles remain a joint validation exercise with network vendors.
