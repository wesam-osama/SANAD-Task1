#  SANAD — CI/CD & DevSecOps Pipeline

> **Task 2 — Training Service CI Pipeline**  
> An automated continuous integration and DevSecOps pipeline implemented for the **SANAD** healthcare platform, ensuring codebase security, secret detection, dependency scanning, and isolated automated testing.

---

##  Table of Contents
- [Overview](#-overview)
- [Pipeline Architecture](#-pipeline-architecture)
- [Key Features & Security Controls](#-key-features--security-controls)
- [Workflow Configuration](#-workflow-configuration)
- [Execution & Verification (Evidence)](#-execution--verification-evidence)
- [How to Run Locally](#-how-to-run-locally)

---

##  Overview

**SANAD** is an integrated doctor-patient medical services and private RAG platform. This repository demonstrates the implementation of a robust **CI Pipeline** for the SANAD backend service, designed to enforce strict security guardrails (Shift-Left Security) and automated testing prior to code integration.

---

##  Pipeline Architecture

The CI pipeline runs automatically on every `push` and `pull_request` to the `main` and `develop` branches. It consists of three decoupled, parallel-friendly jobs:

```text
                  ┌──────────────────────────────┐
                  │      GitHub Trigger          │
                  │   (push / pull_request)      │
                  └──────────────┬───────────────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │                               │
                 ▼                               ▼
    ┌────────────────────────┐      ┌──────────────────────────┐
    │  Secrets Detection     │      │  Dependency & Security   │
    │  (Gitleaks Engine)     │      │  (NPM Audit + Trivy FS)  │
    └────────────────────────┘      └────────────┬─────────────┘
                                                 │
                                                 ▼
                                    ┌──────────────────────────┐
                                    │   Automated Testing      │
                                    │   (Jest + MongoDB Svc)   │
                                    └──────────────────────────┘
