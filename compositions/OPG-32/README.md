# OPG‑32 — Variants Overview (Inference)

Primary profile at this tier is Minimal Inference: no back‑end fabric. Focus on low‑latency front‑end, multi‑tenant overlays, and gateway ingress/egress.

Profiles and variants
- minimal-fe-converged/
  - Front‑end + Storage converged (BF3 2×200G per server, L3MH); In‑band; OoB
  - Gateway emphasized (distributed x86) for NAT/PAT and egress policy

Common attributes
- Gateway: distributed x86; connected to border leaves; per‑tenant policies via VPC + external ACL/firewall
- QoS: RDMA class disabled; prioritize FE/App and Control; protect in‑band
- Optics: OS2 single‑mode DR‑class (default)

Notes
- The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology.
- Assets are placeholders pending population.
- See inference outline for profile selection and SLO guidance.
