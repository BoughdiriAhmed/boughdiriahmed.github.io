---
layout: post
title: "Finite Sample and Asymptotic Estimator Properties in Causal Inference"
date: 2024-01-01
categories: projects
---

This post covers an exploration of finite-sample and asymptotic properties of estimators commonly used in causal inference — in particular, how these properties differ across various estimand types (risk difference, risk ratio, odds ratio) and across data regimes (RCTs vs observational studies).

## Motivation

Standard asymptotic guarantees tell us that well-specified estimators converge to their true values as $n \to \infty$. But in practice, sample sizes are finite — often small — and the gap between finite-sample and asymptotic behavior can be substantial. Understanding this gap is especially important in causal inference, where misestimation has real-world consequences (e.g., over- or under-estimating treatment benefits).

## Key questions

- How quickly do doubly-robust estimators achieve their asymptotic distributions in practice?
- Does the choice of causal measure (RD vs RR vs OR) affect finite-sample bias and variance differently?
- Under what conditions do weighting-based estimators dominate outcome-modeling approaches in small samples?

## Findings

Simulation studies suggest that one-step estimators for the risk ratio exhibit noticeably higher variance in small samples compared to their risk difference counterparts, even when both are asymptotically efficient. This motivates the careful selection of estimator type when sample sizes are limited.

For more detail, see the related paper: [Quantifying Treatment Effects: Estimating Risk Ratios in Causal Inference](https://arxiv.org/abs/2410.12333).
