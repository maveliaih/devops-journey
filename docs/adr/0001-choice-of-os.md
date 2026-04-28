# ADR 0001: Choice of Operating System for Learning Environment

**Status:** Accepted  
**Date:** 2024-04-28

## Context
For the DevOps journey, I need a primary Linux distribution to practice CLI, networking, and service configuration. The choice should balance industry relevance, documentation availability, and stability.

## Options Considered
1. **Ubuntu Server (LTS)**: Debian-based, massive community, industry standard for cloud/web.
2. **CentOS Stream / Rocky Linux**: RHEL-based, standard for enterprise/fintech.
3. **Arch Linux**: Great for deep learning, but high maintenance for a primary lab.

## Decision
I chose **Ubuntu Server 22.04 LTS**.

## Consequences
*   **Pros**: Access to the largest pool of tutorials and community support. Predictable update cycle (LTS).
*   **Cons**: Using `apt` instead of `dnf/yum` (standard in some enterprises), but the core Linux concepts remain universal.
