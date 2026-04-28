# XOC‑64 / 1× OPG‑64 — Minimal Inference (FE+Storage Converged)

## Composed topology

One OPG‑64 building block (8 servers) is placed under an XOC head‑end layer to form a 64‑GPU inference cluster. No back‑end fabric is present. The XOC layer provides distributed gateway infrastructure and external connectivity; all inference traffic flows north‑south through the gateway.

**Frontend fabric:** Each server connects a BF3 2×200G DPU to 2 frontend leaf switches (L3MH). Storage is converged into the frontend fabric. The XOC spine aggregates frontend leaf uplinks and connects to external networks via the distributed gateway.

**Gateway:** Distributed x86 gateway instances attached to border leaves provide NAT/PAT, ingress load distribution, and per‑tenant egress policy via VPC External resources.

**OoB:** Out‑of‑band management is not managed by Hedgehog; site OoB infrastructure connects to BMC/PDU ports.

## Composition attributes

| Attribute | Value |
|-----------|-------|
| Total GPUs | 64 (8 servers × 8 GPUs) |
| Back‑end | None |
| Frontend topology | FE+Storage converged (BF3 2×200G per server, L3MH) |
| Gateway | Distributed x86; connected to border leaves |
| QoS | RDMA class disabled; FE/App and Control prioritized |
| Multi‑tenancy | VPC overlays on FE; per‑tenant External/ExternalAttachment |

## Why this composition

OPG‑64 alone provides the server and leaf‑switch fabric but does not include spine, gateway, or external connectivity. Composing one OPG‑64 under an XOC head‑end adds these layers, making the cluster deployable as a standalone inference endpoint.

Choose this variant when inference workloads run entirely within a single server (no cross‑host coordination needed). The absence of a back‑end fabric reduces cost and complexity; the gateway remains the primary external interface.

## Tradeoffs

- **No cross‑host back‑end:** Inference jobs requiring GPU‑to‑GPU communication across servers cannot use RDMA. All cross‑host traffic must traverse the FE fabric. Use the Distributed variant if cross‑host coordination is required.
- **Gateway is single bottleneck:** All external traffic passes through the distributed gateway layer. Size gateway instances to match peak ingress throughput.

## OPG‑64 building block

This composition uses one instance of OPG‑64 minimal‑fe‑converged. For the building‑block spec, see:
`../../opg-64/minimal-fe-converged/README.md`

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
