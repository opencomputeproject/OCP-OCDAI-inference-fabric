# Using the Inference RA Assets (Scaffold)

This document explains where maintainers (and readers) should place and consume assets for the AI Inference RA.

Folder structure
- `compositions/OPG-<SIZE>/` — size folders (32, 64, 128, 256)
  - `minimal-fe-converged/` — Minimal profile (no back-end)
  - Tokenized variant folders — Distributed profile (with back-end), e.g.,
    - `clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`

Note on cooling and density
- The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology and are not encoded in variant names.

Per-variant assets (drop in the variant folder)
- `connectivity-map.csv` — end-to-end cabling and ports
- `bom.yaml` — bill of materials (switches, optics, cables, gateways)
- `wiring.yaml` — Hedgehog Wiring CRDs (Switch, Server, Connection)
- `vpc.yaml` — Hedgehog VPC CRDs (VPC, VPCAttachment, External, ExternalAttachment)
- `diagrams/` — visuals that match CSV IDs (optional `README.md`)

CSV header and semantics
- Required header (first line):
  `node_type,node_id,port,peer_type,peer_id,peer_port,speed,media_type,network_type,lag_id,plane,comments`
- `node_type`/`peer_type`: one of `switch|server|gateway|border`
- `network_type`: one of `frontend|storage|inband|oob|backend`
- `plane`: blank for Minimal; `A|B` (or `0|1`) for dual-plane designs (rare at ≤256)
- `lag_id`: stable ID for bundled links; empty for unbundled

Minimal vs Distributed specifics
- Minimal (no back-end)
  - Do not include `backend` rows. FE+Storage converged links only, plus in-band and OoB where documented.
  - Include gateway cabling: `node_type=gateway` rows to border leaves; represent north–south policy via VPC `External`/`ExternalAttachment` in `vpc.yaml`.
  - QoS: RDMA class disabled by default; prioritize FE/App and Control; protect in-band/telemetry.
- Distributed (with back-end)
  - Include `backend` rows for scale-out. Use CX7 1×400G per GPU (rail-optimized) as the baseline at these sizes.
  - FE and Storage remain converged; gateway placement identical to Minimal.
  - QoS: RDMA enabled for back-end only; FE/App/Control prioritized as per outline.

CRD consistency rules
- Every `node_id` in `wiring.yaml` must appear in `connectivity-map.csv`.
- `vpc.yaml` must include:
  - Minimal: `External` and `ExternalAttachment` for gateway connectivity; VPC constructs for tenant overlays on FE.
  - Distributed: FE VPC constructs as above; back-end networks modeled with appropriate VPCs/attachments if tenancy spans back-end.

Schemas
- Reuse the schema notes under training RA: `../../training-ra/docs/schema/` (CSV fields, BOM keys, CRD notes).
- Inference adds profile notes only; file formats are identical to training.

Quality checklist (before commit)
- CSV parses with the documented header; LAG/plane fields consistent.
- BOM counts reconcile with connectivity-map rows; gateways included where applicable.
- CRD IDs match CSV `node_id`; gateway `External*` resources present for Minimal and Distributed.
- Diagrams label links using CSV `node_id:port -> peer_id:peer_port` format.
