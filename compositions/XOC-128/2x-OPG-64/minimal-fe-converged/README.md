# XOC‑128 / 2× OPG‑64 — Minimal Inference (FE+Storage Converged)

## Composed topology

Two OPG‑64 building blocks (8 servers each) are connected under a shared XOC spine layer to form a 128‑GPU inference cluster. No back‑end fabric is present. The XOC spine provides inter‑OPG frontend aggregation and connects to external networks via the distributed gateway.

**Frontend fabric:** Each server connects a BF3 2×200G DPU to 2 frontend leaf switches per OPG (L3MH). Frontend leaf uplinks connect to the XOC frontend spine, providing ECMP across all frontend leaves from both OPG‑64 units. Storage is converged into the frontend fabric.

**Gateway:** Distributed x86 gateway instances attached to border leaves provide NAT/PAT, ingress load distribution, and per‑tenant egress policy. A single gateway tier serves both OPG units.

**OoB:** Out‑of‑band management is not managed by Hedgehog.

## Composition attributes

| Attribute | Value |
|-----------|-------|
| Total GPUs | 128 (16 servers × 8 GPUs) |
| Back‑end | None |
| Frontend topology | FE+Storage converged (BF3 2×200G per server, L3MH) |
| XOC spine role | Inter‑OPG FE aggregation; gateway; external egress |
| Gateway | Distributed x86; connected to border leaves |
| QoS | RDMA class disabled; FE/App and Control prioritized |
| Multi‑tenancy | VPC overlays on FE; per‑tenant External/ExternalAttachment |

## Why this composition

Choose this composition over 1× OPG‑128 when you want to grow incrementally (start with one OPG‑64 and add the second later) or when separate OPG procurement and staging is preferred.

Choose this variant (Minimal) when inference workloads run within a single server and no cross‑host GPU coordination is needed. All traffic is north‑south through the gateway.

## Tradeoffs

- **No cross‑host back‑end:** Jobs requiring GPU‑to‑GPU RDMA across servers must use the Distributed variant.
- **Cross‑OPG frontend traffic is spine‑bound:** FE traffic between tenants spanning both OPG units crosses the XOC spine. Tenant placement within a single OPG‑64 avoids this.
- **Gateway is shared:** A single gateway tier serves both OPG units; size gateway instances accordingly.

## OPG‑64 building blocks

This composition uses two instances of OPG‑64 minimal‑fe‑converged. For the building‑block spec, see:
`../../OPG-64/minimal-fe-converged/README.md`

## Assets (placeholders; to be populated)

- `connectivity-map.csv` — end‑to‑end cabling and port mapping
- `bom.yaml` — bill of materials
- `wiring.yaml` — Hedgehog Wiring CRDs
- `vpc.yaml` — Hedgehog VPC CRDs
- `diagrams/` — visuals per fabric

## See also

- Bundle overview: `../README.md`
- OPG‑64 building blocks: `../../OPG-64/README.md`
- Compositions overview: `../../../README.md`
