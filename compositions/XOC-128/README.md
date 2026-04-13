# XOC‑128 — Variants Overview (Inference)

XOC‑128 composes two OPG‑64 building blocks under a shared XOC head‑end layer to form a 128‑GPU inference cluster. The XOC spine provides inter‑OPG frontend aggregation, distributed gateway infrastructure, and external connectivity.

The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology.

Bundles
- [`2x-OPG-64/`](2x-OPG-64/README.md) — two OPG‑64 units under a shared XOC spine

See also
- Compositions overview: [`../README.md`](../README.md)
- OPG‑64 building‑block specs: [`../OPG-64/`](../OPG-64/README.md)
