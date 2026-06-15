# Baseline established: complete beginner in GPU programming

User has never written C++ or CUDA; comfortable enough with Python/ML tooling to pursue an inference-engineer path. Hardware is an Apple M4 Max (48 GB) — no local NVIDIA GPU — and time budget is 10–20 hrs/week for 6 months. This sets the ZPD floor at "performance mental models + first measurements" (not kernels yet), and means every CUDA exercise needs a no-NVIDIA-GPU path (LeetGPU, Colab T4) while MLX/Metal serves as the always-available local lab.

**Implications**
- Lessons 1–8 should require zero C++; introduce C++ only as a CUDA prerequisite (learncpp ch. 1–13), not as a goal.
- The Apple Silicon track is a strength, not a workaround — Moondream ships Core ML/Apple Silicon backends and rejects single-platform candidates. Teach concepts on MLX locally first, then transfer to CUDA in the cloud.
- Honest framing recorded in [[MISSION.md]]: 6 months from zero targets "credible junior inference engineer with public evidence," not direct qualification for a senior end-to-end-ownership role.
