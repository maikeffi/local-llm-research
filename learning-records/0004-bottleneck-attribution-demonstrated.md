# Compute-vs-memory bottleneck attribution: demonstrated empirically

User ran the merged stride benchmark (naive 1-accumulator vs parallel 4-accumulator) and produced a clean result that confirms the whole Phase-1 mental model through their own measurement — this is a milestone, not coverage. They can now predict, measure, and correctly explain whether a workload is compute- or memory-bound.

**Evidence (their output, M4 Max):**
- stride 1–4: 3.2–3.65× speedup (compute/latency-bound — FP-add chain was binding)
- stride 8: 1.84×, stride 16: 1.09× (transition zone)
- stride 32–128: 1.00× (fully memory-bound — breaking the FP chain does nothing)
Single-core sequential floor recovered: stride-1 parallel 0.153 ns/touch → ~26 GB/s, ~5% of the 546 GB/s bus (honest version of "one core can't saturate the bus" — needs ~20× parallelism; GPUs use thousands of threads).

**What is now owned (sets the ZPD floor):**
- Roofline reasoning ([[0002-roofline-measured-on-m4-max]]) applied empirically: the stride sweep walks a workload across the ridge; compute optimizations only pay off right of the ridge.
- Bottleneck attribution discipline ([[0003-bottleneck-attribution-and-prefetcher]]): never name a bottleneck from one number; the speedup column reads out "fraction compute-bound."
- Cache line = 128 B measured cleanly; cache-line/coalescing intuition in place.
- C++ benchmark literacy: ns, stride, the full stride program line by line, -O2, dead-code defeat, per-op normalization, ILP via multiple accumulators.

**Implications**
- Phase 1 (performance foundations) fundamentals are solid and demonstrated. Ready to either (a) make the leap to GPU concretely — run the same reduction on the GPU via MLX/Metal to feel data-parallelism, or (b) continue core CUDA prep. Lean toward the GPU leap next to capitalize on momentum, since the "why GPU" conclusion was just earned by measurement.
- Lesson 0004 updated with the user's actual result table + gradient/roofline tie-in.
- Pedagogy that works for this user: predict → measure → explain, honest self-correction of lesson material, folding their real numbers back into the lesson files.
