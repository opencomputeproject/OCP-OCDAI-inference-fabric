# XOC‑64 / 1× OPG‑64 — Distributed Inference: Rail‑Optimized Clos (CX7 1×400G; BF3 2×200G)

## Composed topology

One OPG‑64 building block (8 servers) is placed under an XOC head‑end layer to form a 64‑GPU inference cluster with back‑end scale‑out capability. The XOC layer provides distributed gateway infrastructure and external connectivity; back‑end RDMA traffic stays within the OPG‑64 rail leaves.

**Back‑end fabric:** Each server connects 8 CX7 1×400G NICs to 8 dedicated backend rail‑leaf switches (rail‑optimized: one NIC per rail). Back‑end RDMA is enabled selectively for cross‑host coordination; most inference traffic remains frontend‑only.

**Frontend fabric:** Each server connects a BF3 2×200G DPU to 2 frontend leaf switches (L3MH). Storage is converged into the frontend fabric.

**Gateway:** Distributed x86 gateway instances attached to border leaves provide NAT/PAT, ingress load distribution, and per‑tenant egress policy.

**OoB:** Out‑of‑band management is not managed by Hedgehog.

## Composition attributes

| Attribute | Value |
|-----------|-------|
| Total GPUs | 64 (8 servers × 8 GPUs) |
| Back‑end topology | Rail‑optimized (8 rail leaves, 1 NIC/GPU/rail) |
| Back‑end NICs | CX7 1×400G per GPU |
| Frontend topology | FE+Storage converged (BF3 2×200G per server, L3MH) |
| Gateway | Distributed x86; connected to border leaves |
| QoS | RDMA enabled for back‑end only; FE/App/Control prioritized |
| Multi‑tenancy | VPC overlays on FE; RDMA isolated to back‑end |

## Why this composition

Choose this variant when inference workloads require cross‑host GPU coordination (e.g., pipeline‑parallel or tensor‑parallel inference spanning multiple servers). The rail‑optimized back‑end keeps cross‑host RDMA leaf‑local within rail domains, minimizing latency.

For workloads that do not require cross‑host coordination, use the Minimal variant to reduce cost and complexity.

## Tradeoffs

- **Back‑end adds cost:** Rail‑leaf switches and CX7 NICs add hardware relative to the Minimal variant. Justified only when cross‑host RDMA is required.
- **RDMA isolated to back‑end:** FE fabric remains multi‑tenant and RDMA‑free, protecting control‑plane and storage latency.
- **All back‑end traffic is leaf‑local:** No spine between rail leaves within a single OPG‑64. Scale beyond 64 GPUs with XOC‑128 (2× OPG‑64).

## OPG‑64 building block

This composition uses one instance of OPG‑64 clos‑ro. For the building‑block spec, see:
`../../OPG-64/clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md`

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
