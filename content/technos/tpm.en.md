---
title: "TPM (Trusted Platform Module)"
description: "A dedicated hardware or firmware chip that provides a root of trust for cryptographic operations, secure key storage, and platform integrity measurements."
tags: ["security", "hardware", "attestation", "boot"]
website: https://trustedcomputinggroup.org/resource/trusted-platform-module-tpm-summary/
related: ["linux_tpm_pcr_registry"]
---

A **Trusted Platform Module (TPM)** is a tamper-resistant security chip — implemented in hardware (dTPM), firmware (fTPM), or software — that acts as a hardware-anchored root of trust for a system. It provides a secure enclave for generating and storing cryptographic keys, performing cryptographic operations, and recording integrity measurements of the boot process.

The TPM's most distinctive feature is its set of **Platform Configuration Registers (PCRs)**: a series of hash accumulators that are extended (not overwritten) during the boot sequence. Firmware, bootloader, kernel, and initrd each contribute measurements to specific PCR banks, building a tamper-evident log of everything that ran before userspace. Standard TPMs expose 24 PCRs; PCRs 0–7 are owned by firmware (UEFI), while PCRs 8–15 are available to the OS. On Linux, these are allocated by convention: PCR 11 is used by `systemd-stub` to measure all UKI components, PCR 12 covers the kernel command line and credentials, PCR 13 covers initrd extension images, and PCR 15 is used for runtime identity measurements like the machine ID and filesystem UUIDs. The authoritative Linux-side allocation is maintained in the [UAPI Linux TPM PCR Registry](https://uapi-group.org/specifications/specs/linux_tpm_pcr_registry/).

PCR values serve two complementary purposes: **forward-looking policy binding**, where a secret is sealed against a known-good PCR state and can only be unsealed if the machine boots identically (enabling automatic disk unlocking via `systemd-cryptenroll`), and **backward-looking attestation**, where a verifier inspects a signed measurement log to confirm that a remote machine ran a specific software stack before granting it access to sensitive resources. TPMs pair naturally with **UKIs** and Secure Boot, and are a foundational component in Confidential Computing, measured boot, and zero-trust infrastructure stacks.
