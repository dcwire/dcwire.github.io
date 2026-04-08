---
layout: page
title: Custom CUDA Extension for PyTorch
description: A PyTorch C++/CUDA extension implementing a fused kernel not available in stock PyTorch
importance: 2
category: cuda
---

> **Status:** Work in progress — fill this in as you build it out.

## Overview

A custom PyTorch extension that wraps a hand-written CUDA kernel using the `torch.utils.cpp_extension` build system. The goal is to implement a fused operation that avoids unnecessary round-trips through GPU global memory that stock PyTorch's eager mode would otherwise produce.

## Motivation

Many ML operations chain multiple elementwise ops (e.g., bias add → activation → dropout). In eager PyTorch, each of these launches a separate kernel and reads/writes the full tensor from/to global memory each time. A fused kernel does all of it in a single pass.

## Implementation

- **C++ binding layer** — `torch::Tensor` interface, input validation, dispatch
- **CUDA kernel** — fused forward pass, templated over dtype
- **Autograd integration** — custom `torch.autograd.Function` with backward pass
- **Benchmarking** — `torch.utils.benchmark` comparison against eager baseline

## Results

| Implementation | Latency (ms) | Memory BW Utilization |
|---------------|--------------|----------------------|
| Eager PyTorch | —            | —                    |
| Fused CUDA    | —            | —                    |

_Fill in with profiling data._

## Code

[Link to GitHub repo](#) _(add link)_
