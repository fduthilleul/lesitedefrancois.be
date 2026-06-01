---
title: "ROCm (Radeon Open Compute)"
description: "AMD's open GPU compute platform—drivers, compilers, and libraries for running PyTorch and inference workloads on Instinct accelerators as an alternative to NVIDIA CUDA on RHEL and OpenShift."
tags: ["ai", "rocm", "amd", "gpu", "cuda", "pytorch", "inference", "training"]
website: https://rocm.docs.amd.com/
---

**ROCm (Radeon Open Compute)** is AMD’s software stack for **GPU compute** on datacenter **Instinct** accelerators (and select consumer GPUs in community setups). Its objective mirrors **CUDA** for NVIDIA: provide kernel compilers (**HIP**), math libraries (rocBLAS, rocFFT), collective communication (**RCCL**, analogous to **NCCL**), and framework integrations so **PyTorch** and inference runtimes can execute training and **inference** on AMD hardware. ROCm is positioned as an open platform (Linux-first) for customers who want accelerator choice or who standardize on AMD in HPC and AI clusters.

Architecturally, HIP source can be written portably from CUDA in many projects; at runtime ROCm talks to the **AMD GPU driver** on **RHEL**, mapping work to compute units and HBM like **CUDA** maps to NVIDIA SMs. The **CPU** still orchestrates launches, dataloader pipelines, and Kubernetes control planes. Not every NVIDIA-optimized kernel or **NIM** container has a ROCm equivalent—ecosystem gaps appear in cutting-edge LLM kernels, though **vLLM** and others expand AMD support over time. Multi-GPU jobs use RCCL over **InfiniBand**/**RoCE** like NCCL. ROCm does not change LLM fundamentals (**KV cache**, batching); it is the execution layer beneath the framework.

**Red Hat** supports ROCm on **Red Hat Enterprise Linux** for validated AMD Instinct configurations, and documents AI workloads on RHEL alongside NVIDIA paths. **OpenShift AI** and GPU operator ecosystems increasingly include AMD device plugins where customers deploy heterogeneous or AMD-only clusters. Red Hat’s value is supported Linux (kABI, SELinux, subscription), Kubernetes scheduling, and reference architectures—not shipping ROCm itself (AMD does). Teams choose ROCm when hardware procurement favors AMD; they choose CUDA/NIM when maximum LLM serving maturity on NVIDIA is required.
