---
title: "UKI (Unified Kernel Image)"
description: "A single portable binary bundling the Linux kernel, initrd, and boot parameters for verified and reproducible boot."
tags: ["boot", "linux", "security", "systemd"]
website: https://uapi-group.org/specifications/specs/unified_kernel_image/
---

A **Unified Kernel Image (UKI)** is a single EFI executable that packages together the Linux kernel, the initramfs (initrd), the kernel command line, and optionally other resources like a splash screen or system credentials. Instead of relying on a bootloader to assemble these components at runtime, a UKI bundles them statically into one signed binary.

This design makes it a natural fit for **Secure Boot**: since the entire boot payload is signed as a unit, any tampering with the kernel, initrd, or boot parameters will break the signature and prevent the system from booting. UKIs are generated and managed by tools like `ukify` (part of systemd) and are central to modern Linux boot security stacks such as those used in Fedora, systemd-boot environments, and projects like `bootc` or Confidential Computing setups. They pair well with **TPM-based measurements** (via PCR registers) for remote attestation.