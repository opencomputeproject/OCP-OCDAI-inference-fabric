# Compositions Overview — AI Inference RA

Welcome. This folder contains compositions for the AI Inference Reference Architecture.

What is an OPG?
- An OPG is a pod‑sized building block: a set of inference servers, storage/metadata services, and the leaf switches they attach to. An OPG does not include the spine/aggregation layer, external gateway, or head‑end connectivity; those are provided by the XOC.

What is an XOC?
- An XOC composes one or more OPGs into a deployable inference cluster by adding the spine/aggregation layer, distributed gateway infrastructure, and external connectivity. If OPGs are adjacent LEGO bricks, an XOC is how you click them together and connect them to the outside world.

Why it matters
- OPGs make it easier to size and plan. XOCs provide the external connectivity, gateway ingress/egress, and inter‑OPG fabric required to operate OPGs as a multi‑tenant cluster, with clear trade‑offs by variant.

How this folder is organized
- OPG catalog: `opg/` contains `opg-32`, `opg-64`, `opg-64-virtual`, `opg-128`, and `opg-256`
- XOC catalog: `xoc/` contains `xoc-64`, `xoc-64-virtual`, `xoc-128`, `xoc-256`, and `xoc-512`
- Each size/tier contains one or more variants. Variant names are tokenized for clarity and grep‑ability.

Profiles
- **Minimal Inference**: No back‑end fabric; FE+Storage converged; gateway is the primary external interface. RDMA class disabled by default; Control/FE traffic prioritized.
- **Distributed Inference**: Adds a back‑end scale‑out network for cross‑host coordination. RDMA enabled for back‑end only; FE remains multi‑tenant.

Assets you'll find in each variant
- `connectivity-map.csv` — end‑to‑end device/port mapping (includes gateway ports)
- `bom.yaml` — bill of materials (switches, optics, cables, gateways)
- `wiring.yaml` — Hedgehog Wiring CRDs (Switch, Server, Connection)
- `vpc.yaml` — Hedgehog VPC CRDs (VPC, VPCAttachment, External, ExternalAttachment)
- `diagrams/` — visuals per fabric

Reading the variant names (quick key)
- Topology: `minimal-fe-converged` (no back‑end), `clos-ro` (rail‑optimized back‑end), `clos-sh` (single‑homed back‑end), `dual-plane` (two independent planes)
- Scale‑out NICs: `cx7-1x400g`, `cx8-2x400g`
- Frontend NICs: `bf3-2x200g`
- Storage links: `storage-conv-<links>x<speed>`

Cooling and density
- The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology.

Virtual learning note
- The virtual learning compositions are intentionally pedagogical. They mirror the RA artifact workflow while using a simplified deployable subset that is suitable for VLAB-based instruction.
