---
title: "TDX (Intel Trust Domain Extensions)"
description: "A CPU-level confidential computing technology that hardware-isolates virtual machines from the hypervisor, host OS, and physical attackers using memory encryption and a dedicated secure arbitration mode."
tags: ["security", "confidential-computing", "hardware", "attestation", "virtualization"]
website: https://www.intel.com/content/www/us/en/developer/tools/trust-domain-extensions/overview.html
---

**Intel Trust Domain Extensions (TDX)** is a confidential computing technology built into Intel CPUs that allows entire virtual machines — called **Trust Domains (TDs)** — to run with hardware-enforced isolation from the host hypervisor, VMM, and any other software on the platform, including privileged system software with administrative access. Unlike **SGX**, which protects small application-level enclaves, TDX operates at the VM level, making it suitable for lifting existing workloads into a confidential environment without significant code changes.

TDX achieves this through two key mechanisms. First, a new CPU operation mode called **SEAM (Secure Arbitration Mode)** hosts the TDX module — a CPU-measured firmware module that sits between the host VMM and the guest TD, managing their separation. The host cannot directly access TD register state or memory; interactions that would normally cause a VMEXIT are instead handled inside the guest via a **Virtualization Exception (#VE)**. Second, all TD private memory is encrypted with a per-TD **AES-XTS 128-bit key** managed by the CPU, ensuring that even physical memory access yields only ciphertext.

For measured boot and attestation, TDX uses **RTMR registers** (Runtime Measurement Registers) — analogous to TPM PCRs but scoped to the TD — to record hashes of the initial TD state, kernel image, firmware, command line, initrd, and ACPI tables. The TD can produce a **TDREPORT**: a CPU-signed structure containing those measurements, which can be forwarded to an Intel SGX Quoting Enclave to produce a remotely verifiable **Quote** for remote attestation. This allows a relying party to verify the exact software stack running inside a TD before sending it sensitive data. TDX is a foundational building block in Confidential Computing stacks and pairs naturally with **TPM**-based and UKI-based measured boot pipelines in Linux guests.

## Additional Information
= [Intel TDX Demystified: A Top-Down Approach](https://dl.acm.org/doi/pdf/10.1145/3652597) (Apr 2024)
