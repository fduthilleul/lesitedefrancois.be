---
title: "Autonomous Networks"
description: "Operator target architectures for self-configuring, self-healing, and intent-driven networks — closed-loop automation, AI/ML in OSS/BSS and the RAN, aligned with TM Forum Autonomous Networks levels and industry zero-touch programmes."
tags: ["telco", "autonomous-networks", "zero-touch", "aiops", "intent-based", "closed-loop", "tm-forum", "oran", "automation"]
website: https://www.tmforum.org/oda/autonomous-networks/
---

**Autonomous Networks (AN)** describe an operator evolution path toward networks that **configure, optimise, secure, and heal themselves** with minimal manual intervention — expressed as **closed loops** (sense → analyse → decide → act) spanning **RAN, transport, core, and cloud infrastructure**. The concept is not a single product but a **maturity model**: **TM Forum** defines **Autonomous Networks Levels (ANL 0–5)**, from fully manual operation (L0) through assisted and partial automation (L1–L3) to high and full autonomy (L4–L5) where **intent** (business or service goals) is translated into technical policies and executed with human oversight only for exceptions. **GSMA** and major operators (e.g. **TM Forum AN Leadership Council** participants) align roadmaps on **high autonomy by ~2027–2030** for selected domains (energy saving, fault recovery, capacity management) rather than overnight “lights-out” operations.

Technically, autonomy composes **telemetry** (PM/FM, streaming, distributed traces), **analytics and AI/ML** (NWDAF in 5GC, **O-RAN RIC** rApps/xApps, vendor SON), **orchestration** (Kubernetes, **ONAP**, **TM Forum Open Digital Architecture**), and **policy/intent engines** that map SLAs to configuration changes validated in **digital twins** or sandboxes before production actuation. **Intent-Based Networking (IBN)** APIs express *what* is required (latency, availability, coverage) while closed loops determine *how* (tilt, power, routing, scaling). **Zero-Touch Provisioning and Management (ZTP, ZSM — ETSI)** provide reference architectures for service and network management automation. Risks — **model drift**, **unsafe actuation**, **opaque AI decisions** — drive requirements for **explainability**, rollback, and **human-in-the-loop** gates at lower maturity levels.

Commercial adoption is **uneven by domain**: **RAN energy optimisation** and **anomaly detection** are among the earliest production closed loops; **end-to-end service provisioning** across multi-vendor stacks remains largely L2–L3. Autonomous Networks intersect heavily with **Open RAN** (programmable RIC), **cloud-native 5GC** (NWDAF, closed-loop NFs), and **AIOps** in IT/cloud operations — but organisational silos (RAN vs core vs IT) often limit cross-domain autonomy more than technology does.

## Additional Information

- [TM Forum Autonomous Networks](https://www.tmforum.org/oda/autonomous-networks/)
- [ETSI ZSM (Zero-touch network and Service Management)](https://www.etsi.org/technologies/zero-touch-network-service-management)
- [GSMA Network Automation](https://www.gsma.com/futurenetworks/)
