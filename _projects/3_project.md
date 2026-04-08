---
layout: page
title: AI Workload Performance Profiling
description: Systematic profiling of training and inference workloads across model architectures using Nsight tools and roofline analysis
importance: 3
category: benchmarks
---

> **Status:** Ongoing — adding new models and configurations as I go.

## Overview

A benchmarking and profiling study of common AI workloads — transformer training, attention inference, and MLP-heavy models — to understand where time is actually spent on GPU and how different configurations (batch size, sequence length, precision) shift the bottleneck.

## What I'm Profiling

- **Transformer attention** — multi-head attention at varying sequence lengths; understanding when it becomes memory-bandwidth-bound
- **MLP blocks** — GEMMs with different shapes and how they map onto the roofline
- **Batch size sweeps** — how occupancy and arithmetic intensity shift as batch size grows
- **Precision modes** — FP32 vs FP16 vs BF16 vs INT8, and the practical throughput difference

## Tools

- **Nsight Compute** — per-kernel metrics: achieved FLOPS, memory bandwidth, warp efficiency, stall reasons
- **Nsight Systems** — end-to-end timeline, CPU/GPU overlap, kernel launch overhead
- **PyTorch Profiler** — operator-level traces, integration with TensorBoard
- **Custom roofline scripts** — plotting arithmetic intensity vs. achieved performance

## Findings

_Document findings here as you accumulate them._

## Code

[Link to GitHub repo](#) _(add link)_
