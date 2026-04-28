# OPG‑32 — Minimal Inference (FE+Storage Converged)

No back‑end fabric. Prioritizes low‑latency north–south traffic, predictable ECMP, and simplified operations. Gateway provides ingress/egress (NAT/PAT) and policy boundaries.

Attributes
- Front‑end + Storage: BF3 2×200G per server (L3MH across two leaves)
- Back‑end: none (single‑server inference)
- In‑band / OoB: present (OoB unmanaged by Hedgehog)
- Gateway: distributed x86 connected to border leaves
- QoS: RDMA class disabled; Control/FE prioritized; protect in‑band/telemetry

Assets (placeholders; to be populated)
- connectivity-map.csv — endpoints, border/gateway cabling, optics
- bom.yaml — switches, optics, cables, gateways
- wiring.yaml — Hedgehog Wiring CRDs (Switch/Server/Connection)
- vpc.yaml — Hedgehog VPC CRDs (VPC, External, ExternalAttachment)
- diagrams/ — visuals matching connectivity IDs

References
- Profile selection and gateway guidance will be published with the RA.
