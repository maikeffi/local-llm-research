# Roofline measured: machine constants established for the M4 Max

User completed the lesson 0002 benchmarks on their M4 Max: **14.2 TFLOP/s** (fp16 matmul), **436 GB/s** (elementwise add, 80% of 546 GB/s nominal — healthy), giving a **ridge point of ≈ 33 FLOPs/byte**. These are now the canonical constants for all future estimates in this workspace.

**Evidence**
Ran the benchmark script and reported numbers unprompted. Asked how to *calculate* the ridge rather than deriving it from the lesson formula — the division itself was walked through in chat (units cancellation: FLOP/s ÷ B/s → FLOPs/byte). Retrieval check (same bandwidth, 2× TFLOPs): correctly reasoned that decode stays bandwidth-bound and compute idles more — the core memory-bound insight is owned. Gaps closed in chat: didn't compute the new ridge (≈65) unprompted, and over-generalized "machine sits idle" to all phases (prefill would in fact ~2× — it's compute-bound). The per-phase split verdict (one hardware change, different effect on prefill vs decode) is the next thing to reinforce.

**Implications**
- Derived planning numbers: fp16 decode crosses the ridge at batch ≈ 33; 4-bit at batch ≈ 8. Reuse these when continuous batching arrives (Phase 5).
- Lessons 0001–0002 are done with real measurements — ZPD now supports starting the C++ track (learncpp ch. 1–4) and deeper Phase 1 material.
- See [[0001-baseline-complete-beginner]] for hardware/time context.
