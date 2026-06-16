# Bottleneck attribution: stride-1 measured FP latency, not bandwidth

User ran lesson 0003's stride experiment on the M4 Max: knee at stride ~128 (512 B, not the textbook 128 B / stride 32), and **0.540 ns/touch at stride 1**. This exposed a misleading claim in the lesson (that stride-1 ns/touch ≈ single-core bandwidth) and became a teaching moment on the single most important inference-engineering discipline: don't name a bottleneck from one number.

Key reasoning surfaced in session:
- 0.540 ns/touch → 7.4 GB/s effective, implausibly low (~1.4% of 546 GB/s) → memory is not the limiter.
- 0.540 ns × ~4.5 GHz ≈ 2.4 cycles/element → fingerprint of the serial `sum +=` fp-add dependency chain (latency-bound compute), not a memory stall.
- Knee at 512 B = hardware prefetcher masking the cache line; a microbenchmark measures cache+prefetcher+TLB together, not one constant.
- Recovery experiment given: 4 independent accumulators to break the dependency chain and reveal the true single-core memory floor.

**Status:** open loop — user has not yet run the 4-accumulator variant. Confirm the predicted speedup next session before treating "separate compute vs memory bottlenecks" as demonstrated rather than just explained.

**Implications**
- Lesson 0003 patched (Section 6 + corrected bonus note) to reflect the honest interpretation.
- User reasons well and pushes on surprising numbers; keep leaning into honest corrections of my own material when reality disagrees — it models the exact skill the role screens for.
- Builds on roofline foundation from [[0002-roofline-measured-on-m4-max]]; baseline/context in [[0001-baseline-complete-beginner]].
