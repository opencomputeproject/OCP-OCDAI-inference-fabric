# XOC‑256 / 2× OPG‑128 — Minimal Inference (FE+Storage Converged)

## Composed topology

Two OPG‑128 building blocks (16 servers each) are connected under a shared XOC spine layer to form a 256‑GPU inference cluster. No back‑end fabric is present. The XOC spine aggregates frontend leaf uplinks from both OPG‑128 units and connects to external networks via the distributed gateway.

**Frontend fabric:** Each server connects a BF3 2×200G DPU to 2 frontend leaf switches per OPG (L3MH). Frontend leaf uplinks connect to the XOC frontend spine, providing cross‑OPG ECMP across all frontend leaves. Storage is converged into the frontend fabric.

**Gateway:** Distributed x86 gateway instances attached to border leaves serve both OPG units, providing NAT/PAT, ingress load distribution, and per‑tenant egress policy.

**OoB:** Out‑of‑band management is not managed by Hedgehog.

## Composition attributes

| Attribute | Value |
|-----------|-------|
| Total GPUs | 256 (32 servers × 8 GPUs) |
| Back‑end | None |
| Frontend topology | FE+Storage converged (BF3 2×200G per server, L3MH) |
| XOC spine role | Inter‑OPG FE aggregation; gateway; external egress |
| Gateway | Distributed x86; connected to border leaves |
| QoS | RDMA class disabled; FE/App and Control prioritized |
| Multi‑tenancy | VPC overlays on FE; per‑tenant External/ExternalAttachment |

## Why this composition

Choose this composition for large-scale gateway‑centric inference where workloads run within individual servers. Two OPG‑128 units under a shared spine doubles capacity while sharing gateway and head‑end infrastructure.

Choose this variant (Minimal) when no cross‑host GPU coordination is needed. For distributed inference requiring RDMA, use the clos‑ro variant instead.

## Tradeoffs

- **No cross‑host back‑end:** RDMA across servers is not supported. Use the Distributed variant for cross‑host GPU workloads.
- **Cross‑OPG FE traffic is spine‑bound:** Tenant traffic between servers in different OPG units crosses the XOC spine. Tenant placement within a single OPG‑128 avoids this.
- **Gateway is shared:** A single gateway tier serves both OPG units; size gateway instances to match aggregate ingress throughput.

## OPG‑128 building blocks

This composition uses two instances of OPG‑128 minimal‑fe‑converged. For the building‑block spec, see:
`../../OPG-128/minimal-fe-converged/README.md`

## Assets (placeholders; to be populated)

- `connectivity-map.csv` — end‑to‑end cabling and port mapping
- `bom.yaml` — bill of materials
- `wiring.yaml` — Hedgehog Wiring CRDs
- `vpc.yaml` — Hedgehog VPC CRDs
- `diagrams/` — visuals per fabric

## See also

- Bundle overview: `../README.md`
- OPG‑128 building blocks: `../../OPG-128/README.md`
- Compositions overview: `../../../README.md`
