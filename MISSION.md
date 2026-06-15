# Mission: Become a Production Inference Engineer

## Why
Qualify for inference engineer roles like [Moondream's](https://moondream.ai/about/careers/inference-engineer) — owning inference performance end-to-end: profiling, custom kernels, kernel fusion, and multi-platform backends (CUDA GPU, Apple Silicon, TPU/Trainium). The 6-month target is to go from zero GPU programming to a credible portfolio of *measured, written-up* inference speedups; senior roles like Moondream's typically also want production experience, so the path optimizes for evidence (benchmarks, blog posts, OSS contributions) that compresses the credibility gap.

## Success looks like
- Can write, profile (Nsight Compute), and optimize a CUDA kernel, explaining the bottleneck in roofline terms
- Can explain and measure prefill vs decode, KV cache, continuous batching, FlashAttention, and PagedAttention — and back each claim with a benchmark run personally
- Has optimized a real model on **two platforms** (CUDA via cloud + Apple Silicon via MLX/Metal on the M4 Max) with before/after numbers
- Has 2–3 public artifacts: blog posts or OSS PRs (e.g. to MLX, vLLM, or Moondream's repo) showing real speedups
- Can pass a GPU-performance interview question cold (e.g. "why is decode memory-bound?", "how would you fuse these ops?")

## Constraints
- Complete beginner: no C++ or CUDA experience yet; strong starting point is Python/ML user level
- Hardware: Apple M4 Max 48 GB (great for MLX/Metal track); CUDA work needs free/cheap cloud (Colab T4, LeetGPU, Lambda/RunPod)
- 10–20 hrs/week for 6 months (≈ 350–450 total hours)

## Out of scope
- Training/pre-training infrastructure (distributed training, FSDP) — inference only
- Quantization as the *primary* tool (Moondream explicitly flags "quantization-only" optimizers as a deal-breaker; treat it as one tool among many)
- ML research / model architecture design
