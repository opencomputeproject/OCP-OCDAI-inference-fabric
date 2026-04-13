# XOC‑512 / 2× OPG‑256 — Distributed Inference: Rail‑Optimized Clos (CX7 1×400G; BF3 2×200G)

## Composed topology

Two OPG‑256 building blocks (32 servers each) are connected under a shared XOC spine layer to form a 512‑GPU inference cluster with back‑end scale‑out capability. The XOC backend spine connects rail‑leaf uplinks from both OPG‑256 units, enabling cross‑OPG RDMA.

**Back‑end fabric:** Each server connects 8 CX7 1×400G NICs to backend rail‑leaf switches per OPG (rail‑optimized). Rail‑leaf uplinks connect to the XOC backend spine, providing cross‑OPG back‑end ECMP. Intra‑OPG back‑end traffic remains leaf‑local.

**Frontend fabric:** Each server connects a BF3 2×200G DPU to 2 frontend leaf switches per OPG (L3MH). Frontend leaf uplinks connect to the XOC frontend spine. Storage is converged into the frontend fabric.

**Gateway:** Distributed x86 gateway instances attached to border leaves serve both OPG units.

**OoB:** Out‑of‑band management is not managed by Hedgehog.

## Composition attributes

| Attribute | Value |
|-----------|-------|
| Total GPUs | 512 (64 servers × 8 GPUs) |
| Back‑end topology | Rail‑optimized Clos (cross‑OPG via XOC spine) |
| Back‑end NICs | CX7 1×400G per GPU |
| Frontend topology | FE+Storage converged (BF3 2×200G per server, L3MH) |
| XOC spine role | Inter‑OPG back‑end ECMP; FE aggregation; gateway; external egress |
| Gateway | Distributed x86; connected to border leaves |
| QoS | RDMA enabled for back‑end only; FE/App/Control prioritized |
| Multi‑tenancy | VPC overlays on FE; RDMA isolated to back‑end |

## Why this composition

Choose this bundle when OPG‑256 procurement is preferred (larger per‑unit footprint). For incremental staging (start with fewer GPUs and expand), prefer the 4× OPG‑128 bundle.

## Tradeoffs

- **Cross‑OPG back‑end traffic is spine‑bound:** Schedule inference jobs within a single OPG‑256 rail domain where possible to minimize spine back‑end traffic.
- **Large footprint per OPG:** Each OPG‑256 unit must be planned and deployed as a complete unit before the second is added.

## OPG‑256 building blocks

This composition uses two instances of OPG‑256 clos‑ro. For the building‑block spec, see:
`../../OPG-256/clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md`

## Assets (placeholders; to be populated)

- `connectivity-map.csv`, `bom.yaml`, `wiring.yaml`, `vpc.yaml`, `diagrams/`

## See also

- Bundle overview: `../README.md`
- OPG‑256 building blocks: `../../OPG-256/README.md`
- Compositions overview: `../../../README.md`
