---
layout: post
title: Writing Your First CUDA Kernel — What They Don't Tell You
date: 2026-04-08 00:00:00
description: The mental model behind thread hierarchy, memory spaces, and why your first kernel is almost certainly memory-bound
tags: cuda gpu performance
categories: kernels
featured: true
---

> **Draft** — replace this with your own content. This is a starter template.

Every CUDA tutorial shows you the same vector addition kernel. It compiles, it runs, and then you're left wondering: why is it slower than just running it on the CPU?

The answer is almost always the same: you wrote a **memory-bound kernel with no reuse**, and you launched it with a thread hierarchy that has no idea how the hardware actually works.

This post is the mental model I wish I'd had on day one.

---

## The Hardware You're Actually Talking To

Before writing a single line of CUDA, it helps to know what you're targeting. An NVIDIA GPU is organized roughly like this:

- **SMs (Streaming Multiprocessors)** — the physical compute units. A modern GPU has tens to hundreds of them.
- **Warps** — groups of 32 threads that execute in lockstep on an SM. This is the real unit of execution, not the thread.
- **Shared memory** — fast, on-chip SRAM local to an SM (~48–100KB depending on config). Orders of magnitude faster than global memory.
- **Global memory** — the big DRAM (HBM on datacenter GPUs). High bandwidth, but high latency.

Your job as a kernel writer is to keep the SMs fed with work and minimize unnecessary global memory traffic.

---

## The Memory Hierarchy Is Everything

A naive kernel looks like this:

```cuda
__global__ void add(float* a, float* b, float* c, int n) {
    int i = blockIdx.x * blockDim.x + threadIdx.x;
    if (i < n) c[i] = a[i] + b[i];
}
```

Every thread reads two values from global memory and writes one. There is zero reuse. The GPU's arithmetic units spend most of their time waiting for memory. This is what "memory-bound" means on the roofline model.

The fix is **data reuse** — either through shared memory (explicit) or by restructuring access patterns so the L2 cache helps you (implicit).

---

## Thread Hierarchy: Blocks and Warps

CUDA threads are organized into blocks, and blocks into a grid. But what actually matters for performance is the warp:

- 32 threads = 1 warp
- All threads in a warp execute the same instruction at the same time (SIMT)
- If threads in a warp take different branches, both paths execute and inactive threads are masked — this is **warp divergence**

When you write `blockDim.x = 256`, you're really saying "launch 8 warps per block." The SM schedules warps, not threads. If one warp is stalled waiting on memory, the SM switches to another — this is **latency hiding**, and it only works if you have enough warps in flight.

---

## What to Measure Before You Optimize

Don't guess. Run Nsight Compute on your kernel and look at:

- **Memory throughput** vs. theoretical peak — are you hitting the roof?
- **Compute throughput** — are your CUDA cores busy?
- **Stall reasons** — `stall_long_sb` means memory latency isn't being hidden; `stall_mio_throttle` means you're hammering the memory system

Once you know which roof you're hitting, you know what to fix.

---

## Next Steps

_Fill in with what you build from here — shared memory tiling, occupancy experiments, etc._
