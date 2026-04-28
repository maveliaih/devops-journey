# ADR 0002: Choice of Virtualization Platform for Local Labs

**Status:** Accepted  
**Date:** 2024-04-28

## Context
I need a reliable way to run Linux instances on my local hardware. The solution must provide stable networking (Host-only, NAT, Bridged) and support snapshots for experiment rollbacks.

## Options Considered
1. **VMware Workstation/Player**: High performance, excellent virtual networking stability.
2. **Oracle VirtualBox**: Open-source, but occasionally has unstable network drivers on some hosts.
3. **Proxmox (Type 1 Hypervisor)**: Great, but requires dedicated hardware which is not available yet.

## Decision
I chose **VMware Workstation**.

## Consequences
*   **Pros**: Rock-solid network isolation, which is crucial for Stage 03 (Networking). Better performance for GUI (when needed).
*   **Cons**: Proprietary software (though a free version for personal use exists).
