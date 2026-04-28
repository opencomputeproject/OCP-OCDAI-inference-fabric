# XOC‑512 — Variants Overview (Inference)

XOC‑512 composes multiple OPG building blocks under a shared XOC spine layer to form a 512‑GPU inference cluster. Two bundle configurations are available depending on OPG procurement preference.

The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology.

Bundles
- [`2x-opg-256/`](2x-opg-256/README.md) — two OPG‑256 units; larger per‑bundle footprint
- [`4x-opg-128/`](4x-opg-128/README.md) — four OPG‑128 units; incremental staging possible

See also
- Compositions overview: [`../README.md`](../README.md)
- OPG‑256 building‑block specs: [`../opg-256/`](../opg-256/README.md)
- OPG‑128 building‑block specs: [`../opg-128/`](../opg-128/README.md)
