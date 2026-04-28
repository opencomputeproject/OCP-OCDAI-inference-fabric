# XOC‑256 / 2× OPG‑128 — Variants

Two OPG‑128 building blocks (16 servers each) are connected under a shared XOC spine layer to form a 256‑GPU inference cluster. The XOC spine aggregates frontend leaf uplinks from both OPG‑128 units, provides cross‑OPG frontend ECMP, and connects to external networks via the distributed gateway.

The compositions in this repository are designed to work with air or liquid cooling at any density.

Variants
- [`minimal-fe-converged/`](minimal-fe-converged/README.md)
  Both OPGs use Minimal profile; no back‑end; gateway‑primary
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md)
  Both OPGs use Distributed profile; rail‑optimized back‑end; inter‑OPG back‑end via spine

See also
- XOC‑256 tier overview: [`../README.md`](../README.md)
- OPG‑128 building‑block specs: [`../../opg-128/`](../../opg-128/README.md)
