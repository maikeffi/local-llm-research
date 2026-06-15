# Inference Engineering Resources

## Knowledge

### Foundations (mental models)
- [Horace He — "Making Deep Learning Go Brrrr From First Principles"](https://horace.io/brrr_intro.html)
  The single best intro to compute-bound vs memory-bound vs overhead-bound. Use for: building the performance mental model before touching CUDA.
- [kipply — "Transformer Inference Arithmetic"](https://kipp.ly/transformer-inference-arithmetic/)
  Back-of-envelope math for inference: FLOPs, memory bandwidth, KV cache size, latency ceilings. Use for: every "what should this cost?" estimate.
- [learncpp.com](https://www.learncpp.com/)
  Free, thorough C++ course. Use for: chapters 1–13 only (enough C++ to write CUDA host/kernel code) — do not complete the whole site.

### CUDA & GPU programming
- [Book: _Programming Massively Parallel Processors_, 4th ed. — Hwu, Kirk, El Hajj](https://www.elsevier.com/books/programming-massively-parallel-processors/hwu/978-0-323-91231-0)
  THE CUDA textbook ("PMPP"). Use for: core curriculum, months 2–3. Chapters 1–6 are the foundation; 7+ as needed.
- [GPU MODE — YouTube lectures + resource stream](https://github.com/gpu-mode/resource-stream)
  Lecture series by working GPU engineers; the resource-stream repo curates papers/blogs. Use for: pairing one lecture per week with PMPP reading. [Lecture 8 notes (CUDA perf checklist)](https://christianjmills.com/posts/cuda-mode-notes/lecture-008/) is a keystone.
- [Simon Boehm — "How to Optimize a CUDA Matmul Kernel"](https://siboehm.com/articles/22/CUDA-MMM)
  Step-by-step worklog from naive matmul to ~cuBLAS performance. Use for: the month-3 capstone — reproduce it kernel by kernel.
- [LeetGPU](https://leetgpu.com/)
  Free in-browser CUDA playground and challenges — no NVIDIA GPU needed. Use for: kernel practice from the Mac before/alongside cloud GPU time.
- [NVIDIA CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/)
  Primary reference. Use for: looking things up, not linear reading.
- [NVIDIA Nsight Compute docs](https://docs.nvidia.com/nsight-compute/)
  The profiler that matters for kernels. Use for: month 3 onward — every kernel you write gets profiled.
- [Triton tutorials](https://triton-lang.org/main/getting-started/tutorials/index.html)
  Python-embedded kernel language used heavily in production (vLLM, PyTorch). Use for: month 4 — fused kernels without full CUDA ceremony.

### Inference systems
- [FlashAttention paper — Tri Dao et al.](https://arxiv.org/abs/2205.14135)
  The canonical "IO-aware kernel fusion" result. Use for: understanding why fusion + memory hierarchy awareness beats raw FLOPs.
- [vLLM docs + PagedAttention paper](https://docs.vllm.ai/)
  Production serving: continuous batching, PagedAttention KV-cache management. Use for: month 5 — read the architecture docs, then source code.
- [FlashInfer blog — "Accelerating Self-Attention for LLM Serving"](https://flashinfer.ai/2024/02/02/introduce-flashinfer.html)
  Kernel library powering modern serving stacks. Use for: seeing how attention kernels are specialized per serving phase.
- [Lilian Weng — "Large Transformer Model Inference Optimization"](https://lilianweng.github.io/posts/2023-01-10-inference-optimization/)
  Survey of the whole toolbox (distillation, quantization, sparsity, batching). Use for: breadth pass and vocabulary.

### Apple Silicon track (your M4 Max)
- [MLX — Apple's ML framework](https://github.com/ml-explore/mlx)
  Array framework for Apple Silicon with custom-kernel support (Metal). Use for: months 1–6 — your local lab for every concept before renting cloud GPUs.
- [mlx-lm](https://github.com/ml-explore/mlx-lm) / [mlx-vlm](https://github.com/Blaizzy/mlx-vlm)
  Run and benchmark LLMs/VLMs locally. Use for: lesson 1 and all local benchmarking.
- [Moondream's open model](https://github.com/vikhyat/moondream)
  The target company's VLM is open source. Use for: capstone — profile and optimize the very model they ship.

## Wisdom (Communities)

- [GPU MODE Discord](https://discord.gg/gpumode)
  THE community for GPU performance work — working-group channels, kernel competitions, direct access to practitioners (many were hired from it). Use for: posting your kernel worklogs, getting reviews, finding collaborators.
- [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA)
  High-traffic local-inference community. Use for: benchmarking norms, what practitioners actually measure, MLX ecosystem news.
- [MLX GitHub Discussions](https://github.com/ml-explore/mlx/discussions)
  Apple Silicon performance questions answered by the MLX core team. Use for: Metal/MLX-specific optimization questions.

## Gaps
- No single high-trust course covers Core ML / ANE deployment deeply; will assemble from Apple WWDC sessions + MLX docs when the platform-breadth phase starts (month 5).
- TensorRT-LLM learning material is mostly NVIDIA docs + samples; revisit when CUDA fundamentals are in place.
