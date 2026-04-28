# XOC‑512 / 2× OPG‑256 — Variants

Two OPG‑256 building blocks (32 servers each) are connected under a shared XOC spine layer to form a 512‑GPU inference cluster. The XOC spine aggregates uplinks from both OPG‑256 units, provides cross‑OPG fabric connectivity, and connects to external networks via the distributed gateway.

The compositions in this repository are designed to work with air or liquid cooling at any density.

Variants
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md)
  Rail‑optimized back‑end; inter‑OPG back‑end via spine

Notes
- Assets are placeholders pending population.
- See the 4× OPG‑128 bundle for an alternative procurement path to 512 GPUs.

See also
- XOC‑512 tier overview: [`../README.md`](../README.md)
- OPG‑256 building‑block specs: [`../../opg-256/`](../../opg-256/README.md)
