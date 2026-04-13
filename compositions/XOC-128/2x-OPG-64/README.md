# XOC‑128 / 2× OPG‑64 — Variants

Two OPG‑64 building blocks (8 servers each) are connected under a shared XOC spine layer to form a 128‑GPU inference cluster. The XOC spine aggregates frontend leaf uplinks from both OPG‑64 units, providing cross‑OPG frontend ECMP, distributed gateway access, and external egress.

The compositions in this repository are designed to work with air or liquid cooling at any density.

Variants
- [`minimal-fe-converged/`](minimal-fe-converged/README.md)
  Both OPGs use Minimal profile; no back‑end; gateway‑primary
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md)
  Both OPGs use Distributed profile; rail‑optimized back‑end; inter‑OPG back‑end via spine

See also
- XOC‑128 tier overview: [`../README.md`](../README.md)
- OPG‑64 building‑block specs: [`../../OPG-64/`](../../OPG-64/README.md)
