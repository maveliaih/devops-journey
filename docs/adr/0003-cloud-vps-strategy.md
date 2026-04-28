# ADR 0003: Strategy for Networking Practice via Cloud VPS

**Status:** Proposed  
**Date:** 2024-04-28

## Context
Local virtualization (VMware) is limited to internal networking. To master DNS, Public IPs, Firewalls (Security Groups), and real-world traffic, practice on a public cloud is required.

## Proposed Solution
Deploy small, cost-effective VPS instances (e.g., DigitalOcean, Hetzner, or AWS Free Tier) specifically for networking and web-server labs.

## Expected Outcomes
*   Mastering SSH hardening in a "wild" environment.
*   Understanding real-world DNS propagation and SSL (Let's Encrypt) issuance.
*   Experience with cloud-provider-specific networking (VPCs, Security Groups).

## Consequences
*   **Pros**: Hands-on experience with production-like environments.
*   **Cons**: Small monthly cost; requires strict security discipline to avoid unauthorized access.
