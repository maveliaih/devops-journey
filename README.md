# DevOps Journey: From Zero to Infrastructure as Code 🚀

Welcome to my technical roadmap. This repository is a comprehensive log of my engineering evolution, documented through hands-on practice, architectural decisions, and custom-built tools.

> [!TIP]
> 🛠 **Featured Project:** [DevOps Flashcards Tool](https://github.io)  
> *A full-stack self-assessment engine covering the entire roadmap: from Git and Linux to Kubernetes, GitOps, and Chaos Engineering. Built to bridge the gap between theory and muscle memory.*

---

## 🏛 Architecture Decision Records (ADR)
I use **ADRs** to document the "Why" behind every technical choice. This ensures that every tool and configuration is a conscious decision, not a default.


| ID | Decision | Status | Key Reason |
|:---:|:---|:---:|:---|
| 001 | [Ubuntu 22.04 LTS](./docs/adr/0001-ubuntu-lts.md) | ✅ Accepted | Industry standard & long-term stability |
| 002 | [VMware Workstation](./docs/adr/0002-vmware-workstation.md) | ✅ Accepted | Reliable networking isolation for local labs |
| 003 | [Cloud VPS Strategy](./docs/adr/0003-cloud-vps-strategy.md) | 💡 Proposed | Real-world DNS & Public IP testing |

---

## 📊 Learning Roadmap & Progress
My journey is divided into logical blocks. Each stage contains lab works, configuration files, and deep-dive analysis.

### 🟢 Fundamentals
- [x] **[Stage 00: Git & GitHub](./stages/stage-00-git)** — Version control & collaboration.
- [ ] **[Stage 01: Linux Fundamentals](./stages/stage-01-linux)** — *Current Focus: OS architecture, CLI & Environment.*
- [ ] **[Stage 02: Bash Automation](./stages/stage-02-bash)** — Scripting & Task automation.
- [ ] **[Stage 03: Networking](./stages/stage-03-networking)** — OSI Model, routing, and VPNs.

### 🟡 Infrastructure & Development
- [ ] **[Stage 04: Docker + Compose](./stages/stage-04-docker)**
- [ ] **[Stage 05: Python for DevOps](./stages/stage-05-python)**
- [ ] **[Stage 06: Advanced Git](./stages/stage-06-git-advanced)**
- [ ] **[Stage 07: Observability](./stages/stage-07-observability)**

### 🔴 Orchestration & CI/CD
- [ ] **[Stage 08: Ansible + CI/CD](./stages/stage-08-ansible-cicd)**
- [ ] **[Stage 09: PostgreSQL + Databases](./stages/stage-09-postgresql)**
- [ ] **[Stage 10: Security Fundamentals](./stages/stage-10-security)**
- [ ] **[Stage 11: Kubernetes](./stages/stage-11-kubernetes)**

### 🛰 Clouds & High Availability
- [ ] **[Stage 12: Cloud + Terraform](./stages/stage-12-terraform)**
- [ ] **[Stage 13: GitOps + ArgoCD](./stages/stage-13-gitops)**
- [ ] **[Stage 14: Kafka + Redis](./stages/stage-14-kafka-redis)**
- [ ] **[Stage 15: System Design](./stages/stage-15-system-design)**
- [ ] **[Stage 16: Chaos Engineering](./stages/stage-16-chaos)**

---

## 📟 Knowledge Base & Insights
Systematized experience and technical deep dives.

*   📑 **Today I Learned (TIL):** Analytical notes on [Environment Variable Hygiene](./docs/til/til-environment-variable-hygiene.md) and [Alias vs Symlink Choice](./docs/til/alias-vs-symlink.md).
*   🚑 **Postmortems:** Detailed incident analysis, e.g., [GitHub Pages Build Failure](./docs/postmortems/postmortem-github-pages-symlink.md).
*   📖 **Runbooks:** Step-by-step guides for environment setup (Work in Progress).

---

## 👤 About the Project
This learning path is built on the **Documentation-driven learning** principle.

*   **Teamwork:** Joint lab sessions and Code Reviews with fellow learners to simulate real-world workflows.
*   **Goal:** Mastering infrastructure automation and building resilient production-ready ecosystems.
