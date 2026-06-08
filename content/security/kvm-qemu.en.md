---
title: "KVM/QEMU"
description: "The standard Linux virtualization stack — KVM accelerates CPU and memory in the kernel, QEMU emulates devices in userspace and drives KVM via ioctl on /dev/kvm; together with libvirt they underpin RHEL, KubeVirt, and OpenShift Sandboxed Containers."
tags: ["virtualization", "linux", "kvm", "qemu", "security", "libvirt", "openshift", "seccomp", "selinux"]
website: https://www.linux-kvm.org
---

**KVM** (Kernel-based Virtual Machine) and **QEMU** (Quick Emulator) solve different halves of the same problem and are almost always used together. **KVM** is a Linux kernel module that turns the kernel into a hypervisor: with **Intel VT-x** or **AMD-V**, guest CPUs run on real hardware at near-native speed and guest memory is managed through extended page tables. KVM has no device model of its own — no disk, network, or firmware emulation. **QEMU** supplies that in userspace (virtio, USB, VGA, ACPI) and controls KVM by issuing **ioctl** calls on **`/dev/kvm`** — creating VMs, mapping memory, running vCPUs via `KVM_RUN` — while **QMP** exposes external management over a Unix socket. **libvirt**, originally from Red Hat, sits above both: it translates **domain XML** into QEMU command lines and lifecycle operations. The stack is the default on Linux: **RHEL** ships `qemu-kvm`, **OpenShift Virtualization** runs **KubeVirt** (`virt-launcher` → libvirt → QEMU), and **OpenShift Sandboxed Containers** uses **Kata Containers** with the same hypervisor to isolate pods in micro-VMs.

The main security concern is not KVM's kernel module — relatively small — but **QEMU's device emulation**: large C codebases parsing untrusted guest input, historically a source of **VM escapes** (e.g. **VENOM**, CVE-2015-3456). Defence in depth matters: run QEMU as the unprivileged `qemu` user, prefer **virtio** over legacy devices, and layer **SELinux** **sVirt** (per-VM MCS labels on QEMU and disk images via **libvirt**), **seccomp** (syscall and **ioctl** allowlists on `/dev/kvm`, vhost, VFIO), and **cgroups**. **KubeVirt** adds pod-level isolation; **Kata** adds a VM boundary so a container escape must cross a guest kernel first. **Confidential VMs** (**SEV-SNP**, **TDX**) go further: guest memory is encrypted so a compromised hypervisor cannot read pod or VM contents in plaintext — the path used by **CoCo** and **Peer Pods** on OpenShift.

Red Hat's supported path remains **KVM/QEMU via libvirt**, not minimal VMMs like **Firecracker** (AWS) or **Cloud Hypervisor** (Kata upstream options with smaller device models). That choice trades a larger emulation surface for the breadth **KubeVirt** needs (TPM, GPU passthrough, live migration) and what **CoCo** needs (virtio-fs, vTPM, TEE launch ioctls). Operational hygiene: keep `qemu-kvm` and libvirt current via RHEL errata, audit domain XML for unnecessary legacy devices, enforce **SELinux** on RHCOS nodes, and use **Trustee** attestation where the threat model includes a hostile infrastructure operator. See also **TCB**, **libvirt**, **Kata Containers**, and **Confidential VM**.

## Additional Information
- [Virtualization in RHEL](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/configuring_and_managing_virtualization/index)
- [QEMU security documentation](https://www.qemu.org/docs/master/system/security.html)
- [libvirt sVirt and SELinux](https://libvirt.org/selinux.html)
- [Deploying OpenShift sandboxed containers](https://docs.redhat.com/en/documentation/openshift_sandboxed_containers/latest/#Deploying%20OpenShift%20sandboxed%20containers)
