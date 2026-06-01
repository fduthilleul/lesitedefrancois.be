---
title: "DPDK"
description: "Data Plane Development Kit: userspace packet I/O framework for high-throughput, low-latency telco VNFs and cloud-native functions — poll-mode drivers, hugepages, and integration with OVS, Kubernetes, and SR-IOV."
tags: ["telco", "dpdk", "dataplane", "userspace", "nfv", "cloud-native", "upf", "performance", "open-source"]
website: https://www.dpdk.org/
---

The **Data Plane Development Kit (DPDK)** is an **open-source** set of libraries and **poll-mode drivers (PMDs)** that move **packet processing** from the kernel to **userspace**, enabling telco and cloud applications to achieve **millions of packets per second** per core with **predictable latency**. DPDK bypasses the traditional socket stack: applications **busy-poll** NIC queues (or **virtio/vhost** rings), use **hugepages** to reduce TLB misses, and pin threads to **NUMA-local** cores — a model suited to **UPF**, **vRouter**, **CG-NAT**, **load balancers**, and **5G user-plane** functions where per-packet syscall overhead is unacceptable.

Core building blocks include **Environment Abstraction Layer (EAL)** for initialization and device discovery, **mbuf** memory pools, **rte_ring** queues, **Hash/LPM/FIB** libraries, **eventdev** and **cryptodev** for pipelines, and **GPU/offload** hooks in newer releases. **PMDs** exist for **Intel**, **Broadcom**, **Mellanox/NVIDIA**, **Marvell**, **virtio**, **vhost-user** (to **OVS** or **VPP**), and **AF_XDP** (hybrid kernel/userspace). Integration patterns:

| **Pattern** | **Description** |
| --- | --- |
| **DPDK on SR-IOV VF** | Dedicated NIC queues to container/VM |
| **vhost-user / virtio-user** | Connection to **OVS-DPDK** or **VPP** |
| **AF_PACKET / AF_XDP** | Lower setup cost; moderate performance |
| **DPDK in Kubernetes** | **Userspace CNI**, device plugins, **Sriov-DPDK** |

**OVS-DPDK**, **FD.io VPP**, **TRex**, and commercial **CNFs** (UPF, firewall) build on DPDK. **Telco cloud-native** packaging often combines **DPDK dataplane** containers with **Kubernetes** **CPU isolation**, **hugepage** `emptyDir`/`limits`, and **IRQ tuning**. Challenges: **CPU consumption** at low load (polling), **debugging** complexity, **kernel bypass** security surface, and **version coupling** between DPDK, NIC firmware, and distro kernels.

DPDK is maintained by the **Linux Foundation** with contributions from **Intel**, **NVIDIA**, **Marvell**, **Red Hat**, and operators; it remains the **de facto** foundation for high-performance userspace networking alongside **eBPF/XDP** for complementary kernel-side fast paths.

## Additional Information

- [DPDK Project](https://www.dpdk.org/)
- [DPDK Programmer’s Guide](https://doc.dpdk.org/guides/prog_guide/)
- [FD.io VPP (often used with DPDK)](https://fd.io/vppproject/vpp/)
