---
title: "DOCA (Data Center Infrastructure on a Chip Architecture)"
description: "NVIDIA's SDK and runtime for programming BlueField DPUs: libraries and services for networking, storage, security, and telemetry so infrastructure functions run on the NIC instead of the host CPU."
tags: ["ai", "doca", "dpu", "nvidia", "bluefield", "networking", "offload", "sdk"]
website: https://developer.nvidia.com/doca-sdk
---

**DOCA (Data Center Infrastructure on a Chip Architecture)** is NVIDIA's software framework for building and operating services on **BlueField DPUs**. Its objective is to standardize how operators and ISVs develop **infrastructure applications**—OVS offload, firewall/VNF, storage targets, RDMA/RoCE control, TLS inspection, telemetry agents—on Arm cores and hardware accelerators embedded in the NIC, using a consistent set of libraries instead of ad hoc kernel modules on the host. DOCA spans drivers, userspace APIs, reference pipelines, and marketplace-packaged applications; it is the DPU counterpart to CUDA on GPUs, oriented toward I/O and packet processing rather than tensor math.

Architecturally, DOCA exposes **programmable pipelines** (match-action tables, flow steering), **Comm Channel** interaction between host and DPU, **GPUNetIO**/RDMA hooks where relevant, and security services (IPsec, TLS, RegEx) that execute on fixed-function blocks. The **host CPU** runs tenant VMs, Kubernetes, and GPU workloads; the **DPU CPU** runs the DOCA runtime and infrastructure containers with a separate root of trust. Compared with implementing the same functions on the host, latency to the wire is lower and blast radius is smaller because compromise of a tenant workload does not automatically grant kernel networking privileges on the dataplane. Compared with a **GPU**, DOCA never targets FP32/FP16 matrix throughput; it targets line-rate packets, connection state, and east-west policy at 100–400 GbE scale.

**Red Hat** supports DOCA in conjunction with **RHEL on BlueField** and OpenShift-based deployments. Operators can run RHEL on the DPU Arm cores, use DOCA applications for accelerated networking and security, and manage the host with the same RHEL/OpenShift lifecycle tooling. Red Hat and NVIDIA publish guidance for **Open vSwitch** offload, **IPsec**, cloud-native networking, and zero-trust segmentation using DOCA on OpenShift. The value for AI platforms is operational: GPU nodes stay focused on models while DOCA-backed DPUs handle cluster networking, storage initiation, and policy enforcement with a supported Linux stack on both sides of the split.

## Additional Informnation
- [DPU-enabled networking with OpenShift and NVIDIA DPF](https://developers.redhat.com/articles/2025/03/20/dpu-enabled-networking-openshift-and-nvidia-dpf#) (Mar 20, 2025)
- [NVIDIA OVS-DOCA on OpenShift](https://schmaustech.blogspot.com/2025/11/nvidia-ovs-doca-on-openshift.html) (Nov 24, 2025)
- [NVIDIA OVS-DOCA via On-Cluster Layer OpenShift](https://schmaustech.blogspot.com/2026/05/nvidia-ovs-doca-via-on-cluster-layer.html) (May 7, 2026)