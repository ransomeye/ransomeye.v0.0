# RansomEye V0.0

### *Project Code Name*

---

## Overview

RansomEye is a Tier-1, air-gap-first cybersecurity system engineered for regulated enterprise environments, including banking infrastructure, defense networks, and forensic-grade deployments.

This repository contains the V0.0 foundational implementation of the RansomEye architecture — a deterministic, CPU-first, and cryptographically verifiable cyber defense platform designed to outperform legacy EDR/XDR systems.

> Important: *RansomEye is a project code name and not a commercial product name.*

---

## Core Principles

RansomEye is built on non-negotiable architectural invariants:

### 1. Air-Gap First

* Operates indefinitely without internet connectivity
* No external APIs, cloud dependencies, or telemetry leakage

### 2. Deterministic Detection

* Identical telemetry + identical model state ⇒ identical output
* No stochastic inference in production detection paths

### 3. CPU-First / Bare-Metal Performance

* Zero-copy data paths (eBPF, mmap, XDP)
* Lock-free concurrency primitives
* SIMD acceleration (AVX2 / AVX-512) for Bayesian inference

### 4. Cryptographic Integrity (WORM)

* AES-256-GCM encryption
* Ed25519 signing
* RFC 6962 Merkle tree audit chains
* Immutable forensic evidence

### 5. Human-in-the-Loop Enforcement

* Autonomous enforcement is disabled by default
* All critical actions require explicit operator policy

---

## System Architecture (High-Level)

```
+------------------------+
|   SOC Dashboard (UI)   |
+-----------+------------+
            |
            v
+------------------------+
|   Core Engine (Go)     |
| - Policy Engine        |
| - API Layer (gRPC)     |
| - Detection Pipeline   |
+-----------+------------+
            |
   -------------------------
   |           |           |
   v           v           v
+------+   +--------+   +--------+
|Agent |   | Probe  |   |  AI    |
|Win/Lx|   |Network |   | Engine |
+------+   +--------+   +--------+
            |
            v
+------------------------+
| PostgreSQL (TLS 1.3)   |
| Redis (Local Only)     |
+------------------------+
```

---

## Repository Scope (V0.0)

This version implements the foundational layers defined across the PRD suite:

* Core Engine Platform (control plane, gRPC API)
* Linux & Windows Agents (telemetry collection)
* DPI Network Probes (NetFlow, Syslog ingestion)
* AI Detection Engine (Bayesian inference, deterministic execution)
* Policy Enforcement Engine (manual-first enforcement model)
* Forensics & Legal Readiness (WORM evidence pipeline)
* Air-Gapped Update Mechanism
* SOC Dashboard (local UI)

---

## Non-Negotiable Constraints

The following are hard invariants enforced across the system:

* TLS 1.3 ONLY — no fallback to TLS 1.2
* Loopback Binding Only — all internal services bind to `127.0.0.1`
* No IPv6 loopback (`::1`) and no `0.0.0.0` exposure
* No external network dependencies
* No undefined database structures (schema strictly PRD-bound)
* No heuristic or non-deterministic detection paths

---

## Technology Stack

| Layer          | Technology                                |
| -------------- | ----------------------------------------- |
| Core Engine    | Go                                        |
| Agents         | Rust / C / C++                            |
| AI/ML          | Python (offline training), SIMD inference |
| Network Probes | Rust (eBPF / DPI)                         |
| Database       | PostgreSQL (TLS 1.3 enforced)             |
| Cache          | Redis (loopback only)                     |
| UI             | React + NGINX (static build)              |

---

## Security Model

* Zero external trust boundaries
* Full internal mutual TLS (TLS 1.3)
* Cryptographically signed telemetry and logs
* Immutable forensic storage
* Offline-first update and validation pipeline

---

## Build & Deployment (Conceptual)

> Full installation and deployment pipelines are defined in PRD-17 (Installer) and PRD-16 (Air-Gapped Updates).

Typical flow:

1. Build binaries (agents, probes, core)
2. Install via controlled installer
3. Initialize local cryptographic material
4. Start core services (loopback-bound)
5. Connect agents and probes
6. Validate deterministic telemetry pipeline

---

## Intended Use

RansomEye V0.0 is designed for:

* High-security enterprise environments
* Air-gapped or restricted networks
* Forensic-grade audit and compliance scenarios
* Advanced ransomware and zero-day threat defense

---

## Status

* Architecture: Defined (PRD-complete)
* Implementation: V0.0 (Foundational)
* Security Model: Strict / Non-Relaxable

---

## License

To be defined (must comply with air-gap distribution and enterprise deployment requirements).

---

## Final Note

RansomEye is not a conventional security product.
It is a provable cyber defense system built on deterministic computation, cryptographic integrity, and zero-trust execution at the architectural level.

Info@RansomEye.Tech
