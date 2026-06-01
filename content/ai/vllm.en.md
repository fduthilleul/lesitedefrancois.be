---
title: "vLLM"
description: "An open-source LLM inference and serving engine that maximizes GPU utilization through PagedAttention, continuous batching, and high-throughput decoding for production chat, RAG, and API workloads on Kubernetes or bare metal."
tags: ["ai", "vllm", "inference", "llm", "gpu", "serving", "kubernetes", "pagedattention"]
website: https://docs.vllm.ai/
---

**vLLM** is an open-source library and serving stack for **large language model (LLM) inference**. Its objective is to turn a trained model into a production service that sustains many concurrent users with low latency and high **tokens per second** per GPU. vLLM targets the inference phase (prefill + decode), not training: it loads weights onto accelerators, batches incoming prompts, schedules decode steps, and streams completions back to clients over HTTP/gRPC (often via an OpenAI-compatible API). It has become a de facto engine behind many private and cloud AI gateways because it ships integrations for Hugging Face models, LoRA adapters, tensor parallelism, pipeline parallelism, speculative decoding, and quantization (GPTQ, AWQ, FP8).

Architecturally, vLLM differs from running a model naively on a **CPU** or a single-threaded GPU script in three ways. First, **PagedAttention** stores the **KV cache** in non-contiguous GPU memory pages (like virtual memory), so batch size and sequence length scale without the fragmentation that wastes VRAM on fixed buffers. Second, **continuous batching** adds and removes sequences from a running batch each iteration instead of waiting for every request in a static batch to finish—critical for chat workloads with uneven lengths. Third, custom **CUDA** kernels and communication backends (NCCL) keep attention and MLP matmuls on the device while the host CPU only orchestrates scheduling and I/O. A CPU-only path exists for tiny models but is not the design center; vLLM assumes **GPU** (or supported accelerator) memory bandwidth and parallelism dominate cost and latency.

**Red Hat** integrates vLLM into **Red Hat OpenShift AI** and **RHEL AI** reference architectures as a supported model-serving option alongside other runtimes. On **OpenShift**, vLLM runs in containers with GPU device plugins, often behind a route or gateway; Red Hat documents validated GPU nodes, drivers, and partner stacks (including **NVIDIA**). **llm-d**, a Kubernetes-native inference project co-led by Red Hat and others, uses vLLM as its default model server and adds cluster-level routing and disaggregation above it. Operators therefore deploy vLLM as the per-pod engine while Red Hat platforms supply Linux, Kubernetes, security (SELinux, SCCs), and MLOps workflows around it.

## Additional Information
- [What is vLLM ?](https://www.redhat.com/en/topics/ai/what-is-vllm)
- [Meet vLLM: For faster, more efficient LLM inference and serving](https://www.redhat.com/en/blog/meet-vllm-faster-more-efficient-llm-inference-and-serving) (Mar 31, 2025)
- [Accelerate AI inference with vLLM](https://www.redhat.com/en/blog/accelerate-ai-inference-vllm) (Sep 19, 2025)
- [How to deploy and benchmark vLLM with GuideLLM on Kubernetes](https://developers.redhat.com/articles/2025/12/24/how-deploy-and-benchmark-vllm-guidellm-kubernetes#) (Dec 24, 2025)
- [5 steps to triage vLLM performance](https://developers.redhat.com/articles/2026/03/09/5-steps-triage-vllm-performance#) (Mar 9,2026)