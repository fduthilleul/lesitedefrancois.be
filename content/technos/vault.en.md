---
title: "Vault (HashiCorp Vault)"
description: "A secrets management system that provides a unified API for storing static secrets, generating dynamic credentials on demand, issuing X.509 certificates, and encrypting data — with every operation authenticated, authorised, audited, and time-bounded."
tags: ["security", "secrets", "key-management", "kubernetes", "pki", "infrastructure"]
website: https://www.vaultproject.io
---

**HashiCorp Vault** is a secrets management platform designed to replace the pattern of static, long-lived credentials scattered across configuration files, environment variables, and CI pipelines with a centralised, policy-enforced, fully audited secrets API. Its core abstraction is that every secret has an identity (a path), an owner (determined by an auth method), a policy (an HCL `HashiCorp Configuration Language` document granting access to specific paths), and a lease (a TTL after which the secret expires or must be renewed). Nothing in Vault is persistent by default — every access is authenticated, every secret access is logged to an immutable audit trail, and credentials that are no longer needed expire automatically rather than accumulating indefinitely.

Vault's most architecturally significant feature is its **secrets engines**: pluggable backends that define how a particular category of secret is generated or stored. The **KV engine** stores static key-value pairs (API keys, passwords) with optional versioning. The **Database engine** generates dynamic credentials — short-lived, unique username/password pairs — directly in a target database (PostgreSQL, MySQL, MongoDB), rotated automatically, so no application ever shares a credential or holds one longer than its lease. The **PKI engine** acts as a certificate authority: it issues X.509 certificates on demand with configurable TTLs (minutes to hours rather than years), eliminating the manual CSR/approval cycle and making certificate rotation a non-event. The **Transit engine** provides encryption-as-a-service — applications encrypt and decrypt data by calling Vault rather than holding a key themselves, and key rotation happens inside Vault without re-encrypting all data at once. On startup, Vault is **sealed**: its encrypted storage is inaccessible because the master key is split into shards using Shamir's Secret Sharing, requiring a quorum of key holders to unseal it. In production, **auto-unseal** via a cloud KMS (AWS KMS, Azure Key Vault) or an **HSM** (via PKCS#11) replaces the manual quorum, allowing Vault to restart without operator intervention while the master key remains hardware-protected.

Vault integrates with Kubernetes through three complementary patterns, each answering a different question: how to **configure** Vault for the cluster, how to **sync secrets into native `Secret` objects**, and how to **deliver secrets as files inside pods**. Platform teams often use **Vault Config Operator (VCO)** or **Terraform** for the first layer, then **VSO** or the **Agent Injector** for workloads. **VSO** and the **Agent Injector** are both HashiCorp-supported; **VCO** is the community [redhat-cop/vault-config-operator](https://github.com/redhat-cop/vault-config-operator) project (common on OpenShift for GitOps Vault admin).

| | **Vault Config Operator (VCO)** | **Vault Secrets Operator (VSO)** | **Vault Agent Injector** |
| --- | --- | --- | --- |
| **Primary role** | Declaratively **configure Vault** (auth mounts, K8s roles, secret engines, policies) | **Sync** Vault secrets into native Kubernetes `Secret` objects | **Inject** Vault secrets as **files** in annotated pods |
| **Vault API use** | Admin / provisioning | Read secrets for workloads | Read secrets per pod |
| **Typical consumer** | Platform / security team | Application teams, GitOps | Apps that read config from disk |
| **Pod changes** | None (cluster-level CRDs) | None (standard `Secret` refs) | Annotations + init/sidecar containers |
| **Secrets in etcd** | Only if using `VaultSecret` CR (overlap with VSO) | Yes — materialised `Secret` objects | Usually no — files on a shared volume |
| **Relation to ESO** | Orthogonal (config vs consumption) | Vault-only; similar consumption model to **ESO** | Orthogonal; file-based alternative |
| **Maintainer** | Community (Red Hat COP) | HashiCorp (supported) | HashiCorp (supported) |

Choose **VCO** (or Terraform) to set up Kubernetes auth, paths, and roles before apps consume secrets. Choose **VSO** (or **ESO**) for standard `envFrom` / `secretKeyRef` workflows at the cost of secrets in the control plane datastore. Choose the **injector** when file-based delivery and keeping secret material out of the Kubernetes API matters.

In the confidential computing stack, Vault occupies a different niche from **Trustee**: Trustee gates secret release on TEE hardware attestation evidence (a **TDX** Quote or **SEV-SNP** report) and is purpose-built for the CoCo threat model where the infrastructure is untrusted; Vault gates secret release on identity and policy (Kubernetes service account, AWS IAM role, AppRole) and is purpose-built for the conventional infrastructure threat model where the platform itself is trusted. The two are complementary rather than competing — a **CoCo** workload might use Trustee to bootstrap a Vault token inside a TEE, then use Vault for all subsequent secret management — and both sit above an **HSM** when the highest assurance key storage is required.

## Additional Information
- [Evolving Kubernetes security with Vault and OpenShift](https://www.youtube.com/watch?v=JiO5TBt_648) (Oct 15, 2025)
- [Automate Secure Secrets in OpenShift with Vault & VSO](https://www.youtube.com/watch?v=G7Fvo4UBaHI) (Dec 16, 2025) 
- [Security model for Vault Kubernetes KMS](https://github.com/hashicorp/web-unified-docs/blob/ab6191e4856b52a59a87fe0f17703671a7317ec6/content/vault/v1.21.x/content/docs/deploy/kubernetes/kms/security.mdx) 
