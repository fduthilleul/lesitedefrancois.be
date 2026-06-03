---
title: "CoCo (Confidential Containers)"
description: "A CNCF project that brings hardware-backed confidential computing to Kubernetes, wrapping each pod in a TEE and treating the Kubernetes control plane itself as untrusted."
tags: ["security", "confidential-computing", "kubernetes", "attestation", "containers", "cncf"]
website: https://confidentialcontainers.org
---

**Confidential Containers (CoCo)** is a CNCF sandbox project that lifts hardware confidential computing — **TDX**, **SEV-SNP**, Intel SGX, IBM Secure Execution — up to the Kubernetes pod level, providing a unified software layer that abstracts away the underlying TEE technology. Its defining trust model is unusually strict: the Kubernetes control plane, the kubelet, the container runtime, and the cloud operator are all treated as **explicitly untrusted**. Only the hardware itself and the workload owner's own supply chain are in scope for trust.

The runtime layer is built on **Kata Containers**: each pod runs inside a lightweight VM, providing a hardware isolation boundary between the pod and the host kernel. On TEE-capable hardware, that VM is itself a confidential VM — a TDX Trust Domain or SEV-SNP guest — so even the hypervisor cannot read or tamper with pod memory. Because the Kubernetes control plane is untrusted, pod specifications delivered by it are not blindly executed; instead, a policy engine inside the confidential VM validates what the control plane claims before acting on it.

Attestation and secret delivery are handled by **Trustee**, CoCo's attestation service stack. Inside the confidential VM, an **Attestation Agent (AA)** collects hardware evidence (a TDX Quote or SEV-SNP attestation report) and presents it to the **Key Broker Service (KBS)**, a relying-party service deployed in a separately trusted environment. The KBS forwards that evidence to an **Attestation Service (AS)** for verification against known-good reference values, and only releases secrets — decryption keys, registry credentials, sealed secrets — to pods that pass. This means container images can be stored encrypted in a public registry and pulled by an untrusted node, with decryption keys only becoming available inside the TEE after successful attestation. CoCo is the primary integration point where the low-level primitives described by **TPM** PCR measurements, **TDX** RTMRs, and **SEV-SNP** launch measurements become meaningful access control at the workload layer.

## Relevant Red Hat blog posts
- [What is the Confidential Containers project?](https://www.redhat.com/en/blog/what-confidential-containers-project) (Oct 7, 2022)
- [Confidential computing use cases](https://www.redhat.com/en/blog/confidential-computing-use-cases) (May 16, 2023)
- [Exploring the OpenShift confidential containers solution](https://www.redhat.com/en/blog/exploring-openshift-confidential-containers-solution) (Sep 1, 2024)
- [Use cases and ecosystem for OpenShift confidential containers](https://www.redhat.com/en/blog/use-cases-and-ecosystem-openshift-confidential-containers) (Sep 8, 2024)
- [Secure AI inferencing: POC with NVIDIA NIM on CoCo with OpenShift AI](https://www.redhat.com/en/blog/secure-ai-inferencing-poc-nvidia-nim-coco-openshift-ai) (Mar 18, 2025)
- [Deploy sensitive workloads with OpenShift confidential containers](https://www.redhat.com/en/blog/deploy-sensitive-workloads-with-openshift-confidential-containers) (Jul 30, 2025)
- [Red Hat OpenShift sandboxed containers 1.12 and Red Hat build of Trustee 1.1 bring confidential computing to bare metal and AI workloads](https://www.redhat.com/en/blog/red-hat-openshift-sandboxed-containers-112-and-red-hat-build-trustee-11-bring-confidential-computing-bare-metal-and-ai-workloads) (Apr 13,2026)
- [Confidential Containers workshop on Microsoft Azure Red Hat OpenShift: Learn interactively](https://www.redhat.com/en/blog/confidential-containers-workshop-microsoft-azure-red-hat-openshift-learn-interactively) (Apr 17, 2026)
