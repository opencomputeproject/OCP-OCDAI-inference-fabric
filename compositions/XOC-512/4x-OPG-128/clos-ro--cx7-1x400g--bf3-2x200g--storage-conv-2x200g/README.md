# XOC‑512 / 4× OPG‑128 — Distributed Inference: Rail‑Optimized Clos (CX7 1×400G; BF3 2×200G)

## Composed topology

Four OPG‑128 building blocks (16 servers each) are connected under a shared XOC spine layer to form a 512‑GPU inference cluster with back‑end scale‑out capability. The XOC backend spine connects rail‑leaf uplinks from all four OPG‑128 units, enabling cross‑OPG RDMA.

**Back‑end fabric:** Each server connects 8 CX7 1×400G NICs to backend rail‑leaf switches per OPG (rail‑optimized). Each rail‑leaf's uplinks connect to the XOC backend spine, providing full‑mesh cross‑OPG ECMP across all four OPG units. Intra‑OPG back‑end traffic remains leaf‑local.

**Frontend fabric:** Each server connects a BF3 2×200G DPU to 2 frontend leaf switches per OPG (L3MH). Frontend leaf uplinks connect to the XOC frontend spine. Storage is converged into the frontend fabric.

**Gateway:** Distributed x86 gateway instances attached to border leaves serve all four OPG units via the shared XOC spine.

**OoB:** Out‑of‑band management is not managed by Hedgehog.

## Composition attributes

| Attribute | Value |
|-----------|-------|
| Total GPUs | 512 (64 servers × 8 GPUs) |
| Back‑end topology | Rail‑optimized Clos (cross‑OPG via XOC spine across 4 units) |
| Back‑end NICs | CX7 1×400G per GPU |
| Frontend topology | FE+Storage converged (BF3 2×200G per server, L3MH) |
| XOC spine role | Inter‑OPG back‑end ECMP; FE aggregation; gateway; external egress |
| Gateway | Distributed x86; connected to border leaves |
| QoS | RDMA enabled for back‑end only; FE/App/Control prioritized |
| Multi‑tenancy | VPC overlays on FE; RDMA isolated to back‑end |

## Why this composition

Choose this bundle over 2× OPG‑256 when incremental staging is preferred — deploy one or two OPG‑128 units initially and expand to four while sharing the same XOC spine infrastructure and gateway layer.

## Tradeoffs

- **Cross‑OPG back‑end traffic is spine‑bound:** Schedule inference jobs within a single OPG‑128 rail domain where possible. Jobs spanning multiple OPG units generate cross‑spine back‑end traffic.
- **Four OPG units to manage:** More individual building blocks than the 2× OPG‑256 bundle, but each unit is smaller and staged independently.
- **RDMA isolated to back‑end:** FE fabric remains multi‑tenant and RDMA‑free across all four OPG units.

## OPG‑128 building blocks

This composition uses four instances of OPG‑128 clos‑ro. For the building‑block spec, see:
`../../OPG-128/clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md`

## Assets (placeholders; to be populated)

- `connectivity-map.csv`, `bom.yaml`, `wiring.yaml`, `vpc.yaml`, `diagrams/`

## See also

- Bundle overview: `../README.md`
- OPG‑128 building blocks: `../../OPG-128/README.md`
- Compositions overview: `../../../README.md`
