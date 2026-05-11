---
layout: about
title: about
permalink: /
subtitle: Software Engineer · GPU Enthusiast

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>📍 Hyderabad, Telangana, India</p>
    <p>✉️ anaswork986.15@gmail.com</p>

latest_posts:
  enabled: true
  scrollable: true
  limit: 3
---

## Hello, I'm Anas

I'm a software engineer interested with what happens at the lowest levels of the GPU stack — where arithmetic throughput, memory bandwidth, and warp scheduling collide to determine whether a kernel runs fast or wastes silicon and how software can be optimized so that it helps run ML models faster.

### What I Work On

My current focus sits at the intersection of **GPU kernel development** and **AI workload performance**:

- Writing and optimizing CUDA/GPU kernels — tiling strategies, shared memory layouts, warp divergence, occupancy tuning
- Profiling AI workloads (training and inference) with tools like Nsight Compute and Nsight Systems to understand where cycles actually go
- Evaluating how different model architectures and batch configurations stress the hardware differently — memory-bound vs. compute-bound regimes, roofline analysis
- Experimenting with kernel fusion, custom attention implementations, and quantized inference paths

### How I Think About Performance

I don't trust intuition when it comes to GPUs. The hardware is too counterintuitive — what looks fast in code can thrash the L2, and what looks slow can pipeline beautifully. My process is: **measure first, hypothesize second, optimize third**. A profiler trace tells more truth than any benchmark number in isolation.

What genuinely excites me is the gap between theoretical peak FLOPS and what workloads actually achieve. Closing that gap — even partially — requires understanding the full picture: the ISA, the memory hierarchy, the scheduler, the interconnect. That depth is what I keep chasing.

### Beyond Kernels

When I'm not reading PTX or staring at roofline plots, I'm usually reading about computer architecture, following developments in hardware design, or finding new workloads to throw at the GPU and see what breaks.

---

If you're working on GPU performance, AI systems, or anything low-level and want to compare notes — reach out.
