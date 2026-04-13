# OPG‑256 — Variants Overview (Inference)

At this tier, Distributed Inference variants are typical when cross‑host coordination is required. Minimal profile is less common but can be supported by using OPG‑128 Minimal clusters in parallel.

Variants
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g/README.md)
  Rail‑optimized Clos back‑end; BF3 2×200G frontend; storage converged

Notes
- The compositions in this repository are designed to work with air or liquid cooling at any density. Cooling medium and rack density are physical deployment choices that do not affect the network topology.
- Assets are placeholders pending population.
- Dual‑plane is optional at ≤256; prefer single‑plane unless requirements dictate otherwise.
