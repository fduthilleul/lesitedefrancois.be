---
title: "Decode"
description: "The autoregressive inference phase that generates output tokens one at a time—reusing the KV cache and typically memory-bandwidth-bound—after prefill has processed the prompt."
tags: ["ai", "decode", "inference", "llm", "kv-cache", "vllm", "throughput", "latency"]
website: https://docs.vllm.ai/en/latest/design/paged_attention.html
---

**Decode** is the second stage of **LLM inference**: after **prefill** has stored keys and values for the prompt, the model generates **one new token per forward pass**, appends it to the sequence, extends the **KV cache**, and repeats until a stop condition (EOS token, max length, or API limit). Its objective is fluent continuation—answer text, code, or tool-call JSON—at acceptable **inter-token latency** and cluster **throughput** (tokens per second across many concurrent sessions). Decode drives the “typing” experience in chat UIs; prefill drives how long users wait before the first character appears.

Architecturally, decode is usually **memory-bandwidth-bound** on the **GPU**: each step touches all model weights for a small amount of new compute, while the **KV cache** grows with total sequence length (prompt + generated tokens). **Continuous batching** in **vLLM** mixes decode steps from many requests in one kernel launch to raise utilization. The **CPU** streams tokens to clients and manages batch scheduling but does not perform the heavy matmuls. **Quantization** and **speculative decoding** target decode cost; **tensor parallelism** adds communication per token on multi-GPU setups. **llm-d** **disaggregated** stacks run decode on pools tuned for memory bandwidth, separate from prefill workers.

**Red Hat** tuning guides for **OpenShift AI** emphasize decode for capacity planning: how many concurrent chats per GPU, effect of **MIG** slice size on cache headroom, and autoscaling on tokens/sec or queue depth. **Guardrails** may scan each decoded chunk or the full completion before returning to users. Production SLOs often specify p99 token latency separately from TTFT (prefill). Red Hat platforms do not change decode algorithms; they host **vLLM**, **NIM**, and **llm-d** with supported drivers and observability on **RHEL**/**OpenShift**.
