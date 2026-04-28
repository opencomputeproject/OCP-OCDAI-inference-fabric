# OPG‑128 — Minimal Inference (FE+Storage Converged)

No back‑end fabric. Prioritize low‑latency FE, predictable ECMP, and gateway services. Upgrade path: add back‑end later if distributed inference is needed.

Attributes
- FE+Storage: BF3 2×200G per server (L3MH)
- Back‑end: none
- In‑band / OoB: present (OoB unmanaged)
- Gateway: distributed x86; per‑tenant policies
- QoS: RDMA class disabled; Control/FE prioritized; protect in‑band/telemetry

Assets (to be generated)
- connectivity-map.csv, bom.yaml, wiring.yaml, vpc.yaml, diagrams/

