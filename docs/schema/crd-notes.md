# Hedgehog CRD Notes (Inference)

Minimal profile:
- No back-end fabric; converged Frontend+Storage VPCs; protect in-band/control traffic.

Distributed profile:
- Includes back-end; enable RoCE class only when needed; tune ECN/PFC and DSCP mappings for inference SLOs.

