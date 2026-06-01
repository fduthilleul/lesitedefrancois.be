---
title: "SR-IOV"
description: "PCI-SIG Single Root I/O Virtualisation: hardware virtual functions for near-native NIC performance in NFV and cloud-native telco workloads — pairing with DPDK, virtio, and Kubernetes device plugins."
tags: ["telco", "sr-iov", "nfv", "cloud-native", "virtualization", "dataplane", "nic", "kubernetes", "performance"]
website: https://pcisig.com/specifications/iov/
---

**SR-IOV (Single Root I/O Virtualisation)** is a **PCI-SIG** specification that lets one physical **PCIe** device (typically a **NIC** or accelerator) expose multiple lightweight **Virtual Functions (VFs)** — each assignable directly to a **VM** or container — while a **Physical Function (PF)** remains for management and global configuration. VFs bypass much of the hypervisor’s software switching path, delivering **lower latency**, **higher throughput**, and more **deterministic** behaviour than **paravirtualised virtio** alone — properties valued in **telco NFV** (vEPC, vRAN CU/DU, firewall, DPI) and in **cloud-native** packet workloads on **Kubernetes**.

Architecture: the **NIC firmware** schedules DMA and queues per VF; the **hypervisor** (KVM, ESXi) or **container runtime** maps VFs via **VFIO** or vendor plugins into guests. **SR-IOV Network Virtualisation (SR-IOV NV)** extensions address **VEPA**, **hairpin**, and **overlay** interactions with **Open vSwitch** or **hardware offload**. In **Kubernetes**, **Multus**, **SR-IOV Network Operator**, and **device plugins** attach VFs to **Pods** as secondary interfaces — often the **data plane** while a **management** interface stays on the CNI overlay.

| **Approach** | **Typical latency / CPU** | **Use case** |
| --- | --- | --- |
| **virtio** | Higher software cost | General workloads, flexibility |
| **SR-IOV VF** | Near bare-metal NIC | UPF, vDU, high PPS VNFs |
| **DPDK on VF** | Userspace poll-mode on dedicated queues | Telco packet pipelines |

Trade-offs include **reduced mobility** (VF pinning to host/NIC), **finite VF counts** per port, **operational complexity** (driver, firmware, NUMA alignment), and **security boundaries** (VF isolation depends on NIC and IOMMU). **DPDK** commonly runs atop SR-IOV VFs; **PTP** hardware timestamping may require specific NIC families. **SmartNICs / DPUs** (BlueField, IPU) extend the model with **programmable pipelines** and **ARM control cores**, blurring the line between SR-IOV and **inline acceleration**.

## Additional Information

- [PCI-SIG SR-IOV](https://pcisig.com/specifications/iov/)
- [Linux VFIO documentation](https://www.kernel.org/doc/html/latest/driver-api/vfio.html)
- [Kubernetes SR-IOV Network Operator](https://github.com/k8snetworkplumbingwg/sriov-network-operator)
