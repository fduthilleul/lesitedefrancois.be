---
title: "Edge Computing"
description: "Distributed compute and application hosting at the network edge — ETSI MEC, 5G UPF local breakout, cloud provider zones, and telco edge for low-latency, data-locality, and real-time industrial workloads."
tags: ["telco", "edge-computing", "mec", "5g", "upf", "latency", "cloud", "industry-4.0", "kubernetes"]
website: https://www.etsi.org/technologies/multi-access-edge-computing
---

**Edge computing** in telecommunications places **compute, storage, and application execution** close to users and devices — at **cell sites**, **regional points of presence**, or **on-prem enterprise locations** — rather than only in distant **hyperscale data centres**. The goal is to reduce **end-to-end latency**, limit **backhaul** load, satisfy **data residency**, and enable **real-time** applications (AR/VR, industrial control, V2X, video analytics) that are impractical with **50–100 ms** round trips to central clouds. In **5G**, edge is tightly coupled to the **user plane**: a **local UPF** on **N6** breakout forwards traffic to an **edge data network (DN)** hosting **MEC applications** without hairpinning through the operator’s core hub.

**ETSI Multi-access Edge Computing (MEC)** defines a reference architecture: **MEC platform** (virtualisation, app lifecycle), **MEC orchestrator**, **MEC app** APIs (**MxP**), and exposure of **RAN information** (radio conditions, location) to applications via standardised services. **3GPP** complements this with **NEF** exposure, **LADN (Local Area Data Network)**, and **ULCL / multi-homed PDU sessions** for selective traffic steering. **Hyperscalers** (**AWS Wavelength**, **Azure Edge Zones**, **Google Distributed Cloud Edge**) and **telco edge** (**Ericsson Edge**, **Nokia MX Industrial Edge**, **Vapor IO**, etc.) offer **Kubernetes** or **VM** footprints at the edge, often **co-located** with **vRAN** or **UPF** on **M-CORD / O-RAN**-style infrastructure.

| **Layer** | **Role** |
| --- | --- |
| **Device / UE** | Generates traffic; may run light edge (e.g. AI on device) |
| **RAN + local UPF** | Anchors session; steers flows to local DN |
| **MEC platform** | Hosts apps, provides RAN exposure APIs |
| **Central cloud** | Training, orchestration, non-latency-sensitive workloads |

**Private 5G**, **Open RAN**, and **cloud-native 5GC** accelerate edge adoption by making **UPF** and **CU/DU** **cloud-packaged** and geographically distributable. Operational challenges include **fragmented footprints** (many small sites), **application portability**, **security zoning** between tenant workloads, and **consistent observability** across edge and core. Edge is not universally required — many 5G services still use **centralised UPF** — but it is **essential** for advertised **ultra-low latency** and **on-site industrial** scenarios.

## Additional Information

- [ETSI MEC](https://www.etsi.org/technologies/multi-access-edge-computing)
- [3GPP TS 23.548 – Edge computing enhancements](https://www.3gpp.org/ftp/Specs/archive/23_series/23.548/)
- [GSMA Edge Computing](https://www.gsma.com/solutions-and-impact/technologies/networks/edge-computing/)
