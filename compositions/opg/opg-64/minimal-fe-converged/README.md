# OPG‑64 — Minimal Inference (FE+Storage Converged)

No back‑end fabric. Focus on latency‑sensitive front‑end traffic and ingress/egress via gateway. Suitable for most enterprise inference where single‑server inference suffices.

Attributes
- Front‑end + Storage: BF3 2×200G per server (L3MH)
- Back‑end: none
- Gateway: distributed x86; policy boundaries externalized (ACL/firewall)
- QoS: RDMA class disabled; protect in‑band

Assets (to be generated)
- connectivity-map.csv, bom.yaml, wiring.yaml, vpc.yaml, diagrams/

