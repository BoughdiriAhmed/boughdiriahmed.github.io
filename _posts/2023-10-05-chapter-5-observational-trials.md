---
layout: post
title: "Chapter 5 — Observational Trials"
date: 2023-10-05
excerpt: "How observational studies differ from RCTs and the challenges of confounding in real-world data."
---

<div class="course-chapter">
<p class="chapter-nav">
  Course: <a href="/blog/">Finite Sample and Asymptotic Estimators in Causal Inference</a>
</p>

<p>Observational studies are empirical investigations. Unlike randomized controlled trials (RCTs), observational studies refrain from direct intervention or manipulation of variables. Instead, observational studies focus on real-world dynamics, often in fields such as epidemiology, social sciences and economics.</p>
<p>One of the main differences with randomized controlled trials is the challenge of managing potential confounding variables due to the inherent susceptibility of unmeasured factors to alter observed associations.</p>
<p>Despite this constraint, the usefulness of observational studies is undeniable. This approach reflects the diversity and variability of the real world, which may not be fully reproduced in the controlled environment of randomized controlled trials.</p>
<p>In the context of observational trials, it is totally unrealistic to assume the assumption of ignorability like in RCTs. This is why calculating the ATE is not as straightforward as in randomized clinical trials. In addition, it is necessary to formulate other hypotheses to decompose the ATE. Thus, in order to compute <span class="math inline">\(\mathbb{E}[Y^{(1)}]\)</span> (resp <span class="math inline">\(\mathbb{E}[Y^{(0)}]\)</span>) in the case of observational studies we need to have the potential outcome for all the individuals given that they took (resp or not) the treatment.</p>
<p>To solve this issue we need to make assumptions under which we can estimate the two expectancies. Let <span class="math inline">\(X_i\in \mathbb{R}^p\)</span> be the vector of confounding variables of the individual <span class="math inline">\(i \in \mathcal{I}\)</span>. We can then define the random variable <span class="math inline">\(X\)</span> as:</p>
<p><span class="math display">\[\begin{align*} X \colon \mathcal{I} &amp; \longrightarrow \mathbb{R}^p \\
    i &amp; \longmapsto X_i
\end{align*}\]</span></p>
<div class="Assumption" id="Unconfoundedness" title="Conditional Exchangeability / Unconfoundedness">
<p></p><details class="Assumption fbx-simplebox fbx-default" open=""><summary><strong>Assumption 5.1: </strong>Conditional Exchangeability / Unconfoundedness</summary><div><span class="math display">\[ T \perp\mkern-9.5mu\perp(Y(0), Y(1)) | X \]</span><p></p>
</div></details>
</div>
<p>Unconfoundedness, also known as the “Conditional Exchangeability” assumption, is the assumption that conditioned on confounding variables there are no unobserved variables that simultaneously influence the treatment assignment and the outcome. Hence, the treatment assignment is independent of the potential outcomes conditioned on pre-treatment variables.</p>
<p>We will now define the propensity score which will be a very useful for the assumptions and estimators that we will be working with.</p>
<div class="Definition" id="propensity-score" title="Propensity score">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 5.1: </strong>Propensity score</summary><div>The propensity score is defined as the conditional probability of treatment given background variables: <span class="math display">\[ e(x) = \mathbb{P}[{T=1|X=x}]\]</span><p></p>
</div></details>
</div>
<p>We can now construct our first theorem with all the previous definitions and assumptions.</p>
<div class="Theorem" id="propensity-score-theorem" title="Propensity Score Theorem">
<p></p><details class="Theorem fbx-simplebox fbx-default" open=""><summary><strong>Theorem 5.1: </strong>Propensity Score Theorem</summary><div>Given positivity, unconfoundedness given <span class="math inline">\(X\)</span> implies unconfoundedness given the propensity score <span class="math inline">\(e(X)\)</span>: <span class="math display">\[ T \perp\mkern-9.5mu\perp(Y(0), Y(1)) | X \Longrightarrow T \perp\mkern-9.5mu\perp(Y(0), Y(1)) | e(X)  \]</span><p></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-5.1">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div>To prove this theorem, we will show that for <span class="math inline">\(t\in \{0,1\},\)</span> <span class="math inline">\(\mathbb{P}[{T|Y^{(t)},e(X)}] = \mathbb{P}[{T|e(X})]\)</span> which is equivalent to <span class="math inline">\(T \perp\mkern-9.5mu\perp(Y(0), Y(1)) | e(X)\)</span>. Now we fix <span class="math inline">\(t \in \{0,1\}\)</span>. Since <span class="math inline">\(T\)</span> is binary, we transform can this probability into an expectation: <span class="math display">\[\begin{align*}
    \mathbb{P}[{T|Y^{(t)},e(X)}] &amp;= \mathbb{E}[{T|Y^{(t)},e(X)}]\\
    &amp;= \mathbb{E}[\mathbb{E}[{T|Y^{(t)},e(X), X}]|Y^{(t)},e(X)]\\
    &amp;= \mathbb{E}[\mathbb{E}[{T|Y^{(t)}, X}]|Y^{(t)},e(X)]\\
    &amp;= \mathbb{E}[\mathbb{E}[{T|X}]|Y^{(t)},e(X)] &amp;&amp; \text{Unconfoundness}\\
    &amp;= \mathbb{E}[\mathbb{P}[{T|X}]|Y^{(t)},e(X)]\\
    &amp;= \mathbb{E}[e(X)|Y^{(t)},e(X)]\\
    &amp;= e(X)
\end{align*}\]</span> We also have: <span class="math display">\[\begin{align*}
    \mathbb{E}[T|e(X)] &amp;= \mathbb{E}[\mathbb{E}[T|X=x, e(X)]|e(X)]\\
    &amp;= \mathbb{E}[\mathbb{E}[T|X=x]|e(X)]\\
    &amp;= \mathbb{E}[e(X)]|e(X)]\\
    &amp;= e(X)
\end{align*}\]</span> Therefore, we have that <span class="math inline">\(T \perp\mkern-9.5mu\perp(Y(0), Y(1)) | e(X)\)</span>.<p></p>
</div></details>
</div>
<p>This theorem was introduced by Rosenbaum and Rubin. It basically states that it is not necessary to condition on the whole random variable <span class="math inline">\(X\)</span> but only on <span class="math inline">\(e(X)\)</span> since the propensity score completely describes <span class="math inline">\(\mathbb{P}[{T|X}]\)</span>.</p>
<p>Another assumption is required on this propensity score, to ensure that the processus in treatment assignment is not completely deterministic, that is for any observation the probability to receive or not the treatment is different from 0 or 1.</p>
<div class="Assumption" id="Overlap" title="Positivity / Overlap">
<p></p><details class="Assumption fbx-simplebox fbx-default" open=""><summary><strong>Assumption 5.2: </strong>Positivity / Overlap</summary><div><span class="math display">\[ \exists \eta \in ]0;1[ ,\forall x \in X(\Omega),  \quad \eta \le e(x) \le 1-\eta \]</span><p></p>
</div></details>
</div>
<p>For all levels of X, all individuals have a positive probability of receiving both the treatment and the control. Put differently, it means that there are no subpopulations with zero or near-zero probabilities of receiving a specific treatment, which is also referred to as overlapping. This contrary to Unconfoundedness is a testable assumption.</p>

</div>
