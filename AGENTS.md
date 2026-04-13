# AGENTS.md
Guidelines for AI agents working on inference-ra.

## Principles
- Mirror the training RA structure; emphasize low latency, multi-tenancy, and gateway ingress/egress.
- Keep work reviewable: small PRs, clear commits.
- Be honest about placeholder status and asset gaps.
- Single source of truth: design decisions live in GitHub issues, not repo docs.

## Variant Naming Convention

Folder token format (ordered):
```
<topo>--<so>--<fe>[--<planes>][--<storage>]
```
- `topo`: `clos-ro` (Clos rail-optimized), `clos-sh` (Clos single-homed), `dual-plane`
- `so` (scale-out NICs): `cx7-1x400g`, `cx8-2x400g` (pattern: `<model>-<ports>x<speed>`)
- `fe` (frontend NICs): `bf3-2x200g` (or `fe-2x200g` for vendor-neutral)
- `planes`: `1p` or `2p` (defaults: clos-sh/ro = 1p; dual-plane = 2p)
- `storage`: `storage-conv-<links>x<speed>` or `storage-ded-<links>x<speed>`

**Cooling and density are NOT encoded in variant names.** The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology.

Examples:
- `OPG-64/clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`
- `OPG-128/clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`

## Profiles

- **Minimal Inference**: No back-end fabric; FE+Storage converged; gateway emphasized. RDMA class disabled by default.
- **Distributed Inference**: Adds a back-end scale-out network for cross-host coordination. RDMA enabled for back-end only.

## File Organization

- `compositions/OPG-<SIZE>/minimal-fe-converged/` — Minimal profile variants
- `compositions/OPG-<SIZE>/<variant>/` — Distributed profile variants (tokenized names above)
- `docs/` — Usage guide and schema references

## Asset Checklist (per variant)

- `connectivity-map.csv` — end-to-end cabling and ports
- `bom.yaml` — bill of materials (switches, optics, cables, gateways)
- `wiring.yaml` — Hedgehog Wiring CRDs
- `vpc.yaml` — Hedgehog VPC CRDs
- `diagrams/` — visuals matching CSV IDs

## When In Doubt
- Ask for clarification.
- Refer to `docs/usage.md` for CSV/BOM format rules.
- Refer to the training RA `docs/COMPOSITION_VARIANT_NAMING_TAXONOMY.md` for the authoritative naming spec.
