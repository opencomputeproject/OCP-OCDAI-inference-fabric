# XOC‑128 / 2× OPG‑64 — Distributed Inference: Rail‑Optimized Clos (CX7 1×400G; BF3 2×200G)

## Composed topology

Two OPG‑64 building blocks (8 servers each) are connected under a shared XOC spine layer to form a 128‑GPU inference cluster with back‑end scale‑out capability. The XOC backend spine connects rail‑leaf uplinks from both OPG‑64 units, enabling cross‑OPG RDMA when required.

**Back‑end fabric:** Each server connects 8 CX7 1×400G NICs to 8 dedicated backend rail‑leaf switches per OPG (rail‑optimized). Each rail‑leaf's uplinks connect to the XOC backend spine, providing cross‑OPG ECMP for back‑end traffic. Intra‑OPG back‑end collectives remain leaf‑local; only cross‑OPG traffic traverses the spine.

**Frontend fabric:** Each server connects a BF3 2×200G DPU to 2 frontend leaf switches per OPG (L3MH). Frontend leaf uplinks connect to the XOC frontend spine. Storage is converged into the frontend fabric.

**Gateway:** Distributed x86 gateway instances attached to border leaves serve both OPG units.

**OoB:** Out‑of‑band management is not managed by Hedgehog.

## Composition attributes

| Attribute | Value |
|-----------|-------|
| Total GPUs | 128 (16 servers × 8 GPUs) |
| Back‑end topology | Rail‑optimized Clos (8 rail leaves per OPG; cross‑OPG via spine) |
| Back‑end NICs | CX7 1×400G per GPU |
| Frontend topology | FE+Storage converged (BF3 2×200G per server, L3MH) |
| XOC spine role | Inter‑OPG back‑end ECMP; FE aggregation; gateway; external egress |
| Gateway | Distributed x86; connected to border leaves |
| QoS | RDMA enabled for back‑end only; FE/App/Control prioritized |
| Multi‑tenancy | VPC overlays on FE; RDMA isolated to back‑end |

## Why this composition

Choose this composition when distributed inference workloads require cross‑host GPU coordination across up to 128 GPUs. The XOC backend spine enables cross‑OPG RDMA while keeping intra‑OPG back‑end traffic leaf‑local.

Choose this over 1× OPG‑128 clos‑ro when incremental scaling (start with one OPG‑64, add the second later) is operationally preferred.

## Tradeoffs

- **Cross‑OPG back‑end traffic is spine‑bound:** Schedule inference jobs within a single OPG‑64 rail domain where possible to keep RDMA leaf‑local. Jobs spanning both OPG units generate cross‑spine traffic.
- **Back‑end adds hardware cost:** Rail‑leaf switches and CX7 NICs are justified only when cross‑host RDMA is required.
- **RDMA isolated to back‑end:** FE fabric remains multi‑tenant and RDMA‑free, protecting control‑plane and storage traffic.

## OPG‑64 building blocks

This composition uses two instances of OPG‑64 clos‑ro. For the building‑block spec, see:
`../../opg-64/clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md`

## Assets (placeholders; to be populated)

- `connectivity-map.csv` — end‑to‑end cabling and port mapping
- `bom.yaml` — bill of materials
- `wiring.yaml` — Hedgehog Wiring CRDs
- `vpc.yaml` — Hedgehog VPC CRDs
- `diagrams/` — visuals per fabric

## See also

- Bundle overview: `../README.md`
- OPG‑64 building blocks: `../../opg-64/README.md`
- Compositions overview: `../../../README.md`
