---
title: "Scepsy"
date: 2026-04-17
description: "Serving Agentic Workflows"
---

# Scepsy: Serving Agentic Workflows Using Aggregate LLM Pipelines

{{< figure src="overview.svg" alt="Scepsy overview" caption="Figure 1: Scepsy system overview." >}}

Agentic workflows are how modern AI systems tackle complex tasks. Instead of a single large language model (LLM) doing everything, a workflow chains several LLMs and tools together — one retrieves information, another reasons about it, a third writes code, etc. This chaining is powerful, but it makes serving these workflows efficiently a real headache.

First, workflows are *unpredictable*. Depending on the input, execution might branch one way or another, fan out across parallel calls, or loop back on itself. You can't know in advance how long any given run will take.
Second, workflows are usually defined in *arbitrary frameworks* with their own quirks, so a serving system can't assume much about their structure.
Third, the LLMs in a workflow typically have *skewed resource demands*. That means GPUs get oversubscribed, and how you share them across models matters a lot for performance.

Scepsy is our new *agentic serving system* that tackles these problems. The key idea is a simple observation: even though the end-to-end latency of a workflow is hard to predict, each LLM's _share_ of the total execution time is pretty stable from run to run. One model might consistently take 40% of the work, another 25%, and so on — the absolute numbers move around, but the proportions don't.

Scepsy turns this observation into a planning tool. It starts by profiling each LLM under different parallelism settings, measuring how they behave at different scales. Then it builds what we call an *Aggregate LLM Pipeline*: a lightweight modelling approach that, given a proposed GPU allocation, predicts the latency and throughput you'd get.

With that predictor in hand, the rest becomes a search problem. Scepsy explores allocations over fractional GPU shares, tensor parallelism degrees, and replica counts, looking for the setup that hits a target throughput with the lowest latency. Once it finds a good allocation, a hierarchical placement heuristic maps it onto the actual cluster — minimizing fragmentation while respecting network topology.

On realistic agentic workflows, Scepsy delivers up to 2.4× higher throughput and 27× lower latency compared to systems that optimize LLMs independently or rely on user-specified allocations.

You can read the full paper on [arXiv](https://arxiv.org/abs/2604.15186).
