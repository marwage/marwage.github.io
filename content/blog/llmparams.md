---
title: "How many parameters fit on your GPU cluster?"
date: 2026-05-11
description: "Interactive calculator for the largest transformer that fits a given GPU cluster"
---

An interactive calculator that estimates the largest transformer that fits on a pooled GPU cluster under Adam mixed-precision training, accounting for weights, gradients, optimizer state, and forward activations.

{{< demo src="/llmparams/" title="GPU cluster parameter calculator" caption="Largest transformer that fits a pooled GPU cluster under Adam mixed-precision training." >}}
