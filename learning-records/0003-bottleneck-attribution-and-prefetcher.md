# Bottleneck attribution: stride-1 measured FP latency, not bandwidth

User ran lesson 0003's stride experiment on the M4 Max: knee at stride ~128 (512 B, not the textbook 128 B / stride 32), and **0.540 ns/touch at stride 1**. This exposed a misleading claim in the lesson (that stride-1 ns/touch ≈ single-core bandwidth) and became a teaching moment on the single most important inference-engineering discipline: don't name a bottleneck from one number.

Key reasoning surfaced in session:
- 0.540 ns/touch → 7.4 GB/s effective, implausibly low (~1.4% of 546 GB/s) → memory is not the limiter.
- 0.540 ns × ~4.5 GHz ≈ 2.4 cycles/element → fingerprint of the serial `sum +=` fp-add dependency chain (latency-bound compute), not a memory stall.
- Recovery experiment given: 4 independent accumulators to break the dependency chain and reveal the true single-core memory floor.

**Correction (full table, session 2026-06-17):** earlier "knee at 512 B / prefetcher masking" was wrong — based on a terse first message. The complete stride sweep shows flat ~0.5 ns through stride 16, then a 4.3× cliff at stride 32 (128 B): the cache line is cleanly **128 bytes**, the textbook result. Prefetcher still explains the cheap pre-cliff rows and the gradual post-cliff creep, but does not hide the line size. Lesson 0003 Surprise 2 patched accordingly.

**Status:** open loop — user paused to consolidate fundamentals (asked what ns/stride/the code mean) before running the 4-accumulator variant. Produced lesson 0004 (line-by-line decode + merged naive-vs-parallel benchmark). Still need the user's speedup column (predict: big win at stride 1, ~no win at stride 64) to treat "separate compute vs memory bottlenecks" as demonstrated, not just explained.

**Implications**
- Lesson 0003 patched (Section 6 + corrected bonus note) to reflect the honest interpretation.
- User reasons well and pushes on surprising numbers; keep leaning into honest corrections of my own material when reality disagrees — it models the exact skill the role screens for.
- Builds on roofline foundation from [[0002-roofline-measured-on-m4-max]]; baseline/context in [[0001-baseline-complete-beginner]].
