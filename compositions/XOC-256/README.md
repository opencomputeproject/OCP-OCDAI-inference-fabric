# XOC‑256 — Variants Overview (Inference)

XOC‑256 composes two OPG‑128 building blocks under a shared XOC spine layer to form a 256‑GPU inference cluster. The XOC spine provides inter‑OPG frontend aggregation, distributed gateway infrastructure, optional inter‑OPG back‑end connectivity, and external egress.

The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology.

Bundles
- [`2x-OPG-128/`](2x-OPG-128/README.md) — two OPG‑128 units under a shared XOC spine

See also
- Compositions overview: [`../README.md`](../README.md)
- OPG‑128 building‑block specs: [`../OPG-128/`](../OPG-128/README.md)
