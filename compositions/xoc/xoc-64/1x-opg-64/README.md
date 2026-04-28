# XOC‑64 / 1× OPG‑64 — Variants

This bundle places a single OPG‑64 under an XOC head‑end layer to form a 64‑GPU inference cluster. The XOC layer adds the distributed gateway, spine aggregation, and external connectivity that the OPG‑64 building block does not supply on its own.

The compositions in this repository are designed to work with air or liquid cooling at any density.

Variants
- [`minimal-fe-converged/`](minimal-fe-converged/README.md)
  No back‑end fabric; FE+Storage converged; gateway‑primary
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md)
  Adds rail‑optimized back‑end for distributed inference workloads

See also
- XOC‑64 tier overview: [`../README.md`](../README.md)
- OPG‑64 building‑block specs: [`../../opg-64/`](../../opg-64/README.md)
