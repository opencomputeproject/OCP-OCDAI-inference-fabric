# XOC‑512 / 4× OPG‑128 — Variants

Four OPG‑128 building blocks (16 servers each) are connected under a shared XOC spine layer to form a 512‑GPU inference cluster. The XOC spine aggregates uplinks from all four OPG‑128 units, providing cross‑OPG fabric connectivity, distributed gateway access, and external egress.

This bundle supports incremental staging: begin with one or two OPG‑128 units and add more over time, sharing the same XOC spine infrastructure.

The compositions in this repository are designed to work with air or liquid cooling at any density.

Variants
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md)
  Rail‑optimized back‑end across four OPG‑128 units

Notes
- Assets are placeholders pending population.
- See the 2× OPG‑256 bundle for an alternative with a larger per‑OPG footprint.

See also
- XOC‑512 tier overview: [`../README.md`](../README.md)
- OPG‑128 building‑block specs: [`../../opg-128/`](../../opg-128/README.md)
