# AI Inference Reference Architecture — Assets Repository (Preview Layout)

![OCP](https://img.shields.io/badge/OCP-aligned-blue)
![EVPN/VXLAN](https://img.shields.io/badge/Overlay-EVPN%2FVXLAN-green)
![SONiC](https://img.shields.io/badge/NOS-SONiC-lightgrey)
![Gateway](https://img.shields.io/badge/Component-Gateway-purple)

This repository models the open assets for the AI Inference Reference Architecture (RA). It mirrors the training RA structure but emphasizes low latency, multi‑tenancy, and gateway ingress/egress.

Highlights
- Practical assets per variant: connectivity maps (CSV), BOMs (YAML), Hedgehog CRDs (wiring.yaml, vpc.yaml), and diagrams.
- Clear profiles: Minimal (no back‑end; FE+Storage converged) and Distributed (adds back‑end where needed).
- Gateway guidance: distributed x86 placement, NAT/PAT, and policy via VPC `External` resources.
- QoS notes: FE/App and Control prioritization; RDMA enabled for back‑end only in Distributed.

Profiles
- Minimal Inference: No back‑end fabric; Front‑end+Storage converged; In‑band + OoB. Gateway is core. RDMA class disabled by default; Control/FE prioritized.
- Distributed Inference: Adds a back‑end scale‑out network for cross‑host coordination. RDMA enabled selectively for back‑end; front‑end stays multi‑tenant.

Navigation
- Catalog index: see `../../docs/catalog.md`
- Compositions overview: `compositions/README.md`
- OPG building blocks: `OPG-32`, `OPG-64`, `OPG-128`, `OPG-256` — see `compositions/OPG-*/README.md`
- XOC composed clusters: `XOC-64`, `XOC-128`, `XOC-256`, `XOC-512` — see `compositions/XOC-*/README.md`

What’s inside (diagram)
- See `compositions/OPG-64/diagrams/README.md` for diagram usage. A top‑level overview diagram will be added in a future update.

Cooling and density
- The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology.

Status
- This is a scaffold. Assets are placeholders and will be populated. Tokens mirror training where a back‑end exists; Minimal variants focus on FE+Storage and gateway assets.

How to use
- Start with `docs/usage.md` for CSV header, gateway notes, and profile specifics.
- Pick a size above and open the composition README.
- Within a variant folder, adapt CSV/BOM and review CRDs; apply in lab: `kubectl apply -f wiring.yaml && kubectl apply -f vpc.yaml`.

Rail‑Optimized Benefits (When Back‑End Is Present)
- Wiring allocation keeps all NICs of a given rail index on the same leaf (or contiguous leaves at scale) without changing switch counts.
- Scheduling tenants within a common first‑hop rail domain keeps most scale‑out traffic leaf‑local, dramatically reducing spine traffic and uplink congestion—the chief source of performance issues in large clusters.
- Placement guidance: Pack inference jobs that require back‑end into first‑hop rail domains when possible; misaligned placement forces scale‑out via the spine. Use QoS/ECN/PFC to protect FE/control even as scale‑out bursts occur.

References
- XOC‑N & OPG‑M style references: see the training RA README.
