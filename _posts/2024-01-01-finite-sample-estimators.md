---
layout: post
title: "Finite Sample and Asymptotic Estimator Properties in Causal Inference"
date: 2024-01-01
---

This post covers an exploration of finite-sample and asymptotic properties of estimators in causal inference — in particular, how these properties differ across estimand types (risk difference, risk ratio, odds ratio) and across data regimes (RCTs vs observational studies).

## Motivation

Standard asymptotic guarantees tell us that well-specified estimators converge to their true values as $n \to \infty$. But in practice, sample sizes are finite and the gap between finite-sample and asymptotic behavior can be substantial.

For more detail, see the related paper: [Quantifying Treatment Effects: Estimating Risk Ratios in Causal Inference](https://arxiv.org/abs/2410.12333).
