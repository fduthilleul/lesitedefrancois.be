---
title: "InfiniBand"
description: "Lossless RDMA-native cluster fabric for low-latency GPU collective traffic—standard in large-scale AI training and in llm-d disaggregated inference when moving KV state between nodes."
tags: ["ai", "infiniband", "rdma", "networking", "nccl", "distributed-training", "hpc"]
website: https://www.infinibandta.org/
---

**InfiniBand** is a high-performance **network fabric** designed for datacenter and HPC clusters, natively supporting **RDMA** (Remote Direct Memory Access) with low latency, high bandwidth, and features such as adaptive routing and congestion control at the link layer. Its objective in **AI** is to connect many **GPU** servers so **distributed training** (gradient all-reduce via **NCCL**) and multi-node **inference** (tensor parallel, **llm-d** prefill/decode **KV** transfer) are not limited by TCP overhead on a **CPU**. InfiniBand NICs (e.g. NVIDIA ConnectX) present verbs APIs; subnets are managed with an **Subnet Manager** and partitioned for multi-tenant isolation.

Architecturally, InfiniBand differs from Ethernet in purpose-built **RDMA** semantics and historically simpler lossless delivery within a well-designed fabric—though **RoCE** brings RDMA to Ethernet for customers who want converged networks. A **CPU** is not in the hot path for large transfers once queues are posted; GPUs or their NIC peers move data directly. Compared with **NVLink** inside a server, InfiniBand is the **east-west cluster** plane. Bandwidth planning (HDR, NDR, XDR generations), cable/plan topology, and PKey or tenant isolation are core ops skills. Kubernetes passes IB devices to training or inference pods via device plugins and tuned CNIs on **OpenShift**.

**Red Hat** supports InfiniBand on **RHEL** (drivers, IPoIB where needed, RDMA core) and documents HPC/AI cluster networking for OpenShift and bare metal. Telco and AI reference architectures on Red Hat stacks assume IB or high-end RoCE for scale-out **training** and for **llm-d**-style disaggregation. Red Hat integrates the OS and orchestration layer; Mellanox/NVIDIA and switch vendors document certified leaf-spine designs. Customers run the same SELinux-hardened RHEL on GPU nodes whether the fabric is IB or RoCE.
