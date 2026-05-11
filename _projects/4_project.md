---
layout: page
title: Tiled Matrix Multiplication in CUDA
description: Hand-written CUDA kernel exploiting shared memory tiling to approach cuBLAS throughput on SGEMM
importance: 4
category: cuda
---

> **Status:** Work in progress — fill this in as you build it out.

## Overview

A from-scratch implementation of SGEMM (single-precision general matrix multiplication) in CUDA, progressively optimized from a naive global-memory kernel to a tiled shared-memory implementation.

## Optimization Progression

1. **Naive kernel** — each thread reads directly from global memory, zero reuse
2. **Shared memory tiling** — threads in a block cooperatively load tiles into `__shared__` memory, reducing global memory traffic by a factor of tile size
3. **Thread coarsening** — each thread computes a 2×2 or 4×4 output tile to improve arithmetic intensity
4. **Vectorized loads** — use `float4` loads to maximize memory bandwidth utilization

## Key Metrics

| Kernel | GFLOPS | % of cuBLAS |
|--------|--------|-------------|
| Naive  | —      | —           |
| Tiled  | —      | —           |
| Coarsened | —   | —           |

_Fill in with Nsight Compute results._

## What I Learned

- How shared memory bank conflicts arise and how to avoid padding
- The relationship between tile size, occupancy, and register pressure
- How to read roofline plots and identify whether a kernel is memory-bound or compute-bound

## Code

[Link to GitHub repo](#) _(add link)_
