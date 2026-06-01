---
title: "NVLink"
description: "NVIDIA's high-bandwidth GPU–GPU and GPU–CPU interconnect within a server or NVLink switch tray—essential for tensor-parallel LLM inference and multi-GPU training without traversing PCIe or the network."
tags: ["ai", "nvlink", "nvidia", "gpu", "interconnect", "tensor-parallelism", "training"]
website: https://www.nvidia.com/en-us/data-center/nvlink/
---

**NVLink** is NVIDIA’s proprietary **high-speed interconnect** between GPUs (and, on some platforms, between GPUs and CPUs) inside a server or across an **NVLink switch** system (e.g. NVL72-class racks). Its objective is to move tensors—activations, gradients, **KV cache** shards, or partial attention results—at much higher bandwidth and lower latency than **PCIe** or general **Ethernet**, so multi-GPU **training** and large-model **inference** (tensor parallelism) are not bottlenecked on the bus. NVLink domains define which GPUs can treat each other’s memory as peer-accessible for **CUDA** and **NCCL** without leaving the box.

Architecturally, NVLink is **intra-node** (or intra-tray) fabric, distinct from **InfiniBand**/**RoCE** **RDMA** that links servers. A **CPU** still initiates work, but bulk GPU–GPU copies use NVLink while the host PCIe bus carries I/O and smaller control messages. LLMs that exceed one GPU’s HBM are sharded across NVLink-connected devices; decode and prefill latency for tensor-parallel serving depend on all-reduce and attention communication over that link. **MIG** slices on one physical GPU do not extend NVLink as a multi-GPU pool—they partition a single card. When jobs span nodes, **NCCL** uses network RDMA; within the node, NVLink dominates.

**Red Hat** documents multi-GPU **RHEL** and **OpenShift** nodes where NVLink topology is exposed to schedulers (NUMA, GPU affinity) and partner reference architectures (NVIDIA DGX, HGX) under Red Hat support matrices. **OpenShift AI** capacity planning assumes NVLink-aware placement for large models served via **vLLM** tensor parallel or **NIM** multi-GPU profiles. Operators verify BIOS, firmware, and driver bundles on certified hardware so NVLink lanes train at expected width—platform validation on RHEL, not a separate Red Hat product.
