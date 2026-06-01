---
title: "NCCL (NVIDIA Collective Communications Library)"
description: "Optimized multi-GPU and multi-node collective primitives (all-reduce, broadcast, all-gather)—the communication layer beneath distributed PyTorch training and many multi-GPU LLM inference stacks."
tags: ["ai", "nccl", "nvidia", "distributed-training", "gpu", "infiniband", "roce", "cuda"]
website: https://developer.nvidia.com/nccl
---

**NCCL (NVIDIA Collective Communications Library)** implements **collective operations**—**all-reduce**, **broadcast**, **reduce-scatter**, **all-gather**, and others—optimized for **NVIDIA GPUs** across **NVLink** within a node and **RDMA** (**InfiniBand** or **RoCE**) across nodes. Its objective in **AI** is to make **distributed training** and multi-GPU **inference** (tensor parallelism) scale: gradient shards must merge every step; attention and MLP partitions must exchange activations with minimal latency. Frameworks (**PyTorch** DDP/FSDP, **vLLM** tensor parallel) call NCCL (or delegate to it) rather than hand-rolling socket code.

Architecturally, NCCL selects **transport** based on topology discovery: NVLink peer copies inside the server, then network RDMA between servers, with **CUDA** streams overlapping communication and compute where possible. The **CPU** launches NCCL kernels and progress threads but avoids copying full tensors through host memory on the hot path. **AMD** stacks use **RCCL** instead; NCCL is NVIDIA-specific. Performance depends on **NCCL** environment variables, NIC count, rail-optimized topology, and whether traffic shares congested Ethernet without lossless QoS. NCCL is not a user-facing API for app developers but is mandatory plumbing for large **LLM** jobs.

**Red Hat** supports NCCL indirectly through validated **RHEL** + NVIDIA driver + **CUDA** stacks on GPU servers and **OpenShift** AI training/inference guides. Multi-node job manifests (MPI, PyTorch operator, Slurm on RHEL HPC images) assume NCCL-over-IB/RoCE is correctly wired. Red Hat documentation emphasizes node labeling, huge pages, and driver versions from the support matrix; NVIDIA ships NCCL releases tied to CUDA versions. **llm-d** and **vLLM** multi-node serving likewise depend on healthy NCCL when tensor parallel spans hosts.
