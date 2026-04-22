---
layout: post
title: "Chapter 2 — Potential Outcomes"
date: 2023-10-02
excerpt: "The Neyman-Rubin potential outcomes framework and the fundamental problem of causal inference."
---

<div class="course-chapter">
<p class="chapter-nav">
  Course: <a href="/blog/">Finite Sample and Asymptotic Estimators in Causal Inference</a>
</p>

<section class="level2" data-number="2.1" id="potential-outcomes">
<h2 class="anchored" data-anchor-id="potential-outcomes" data-number="2.1"> Potential outcomes</h2>
<p>The notations we consider are grounded in the potential outcomes framework, a framework initiated by Neyman in 1923 for Randomized Controlled Trials (RCT), and then popularized in the 70’s by Rubin.</p>
<p>Consider an individual <span class="math inline">\(i\)</span>. We denote <span class="math inline">\(T_{i}\)</span> the random variable corresponding to the treatment assignment, which takes values 1 if the individual is treated and 0 otherwise, that is <span class="math inline">\(T_{i} \in \{0,1\}\)</span>. We also define <span class="math inline">\(Y_{i}^{(1)}\)</span> (resp <span class="math inline">\(Y_{i}^{(0)}\)</span>) as the potential outcome of this individual if the treatment was given (resp not given).</p>
<p><span class="math display">\[
    Y_{i}^{(\text{\tiny obs})}={Y_{i}^{(T)}}=\left\{\begin{array}{ll}
    {Y_{i}^{(0)}} &amp; {\text { if } T_{i}=0} \\
    {Y_{i}^{(1)}} &amp; {\text { if } T_{i}=1}
    \end{array}\right.
\]</span></p>
<p>As a consequence, for this individual, we also have one missing potential outcome, denoted by <span class="math inline">\(Y^{(\text{\tiny mis})}\)</span>: <span class="math display">\[
        Y^{(\text{\tiny mis})}={Y^{(1-T_i)}}=\left\{\begin{array}{ll}
        {Y_{i}^{(1)}} &amp; {\text { if } T_{i}=0} \\
        {Y_{i}^{(0)}} &amp; {\text { if } T_{i}=1}
        \end{array}\right.
\]</span></p>
<p>In order to know if the treatment is effective or not for this individual we are interested in <span class="math inline">\(\delta_{i} = Y_{i}^{(1)} - Y_{i}^{(0)}\)</span>, the individual treatment effect (ITE). However, by allocating treatment (<span class="math inline">\(T_{i}=1\)</span>) or control (<span class="math inline">\(T_{i}=0\)</span>) to this individual, one can only one out of the two potential outcomes, which is either <span class="math inline">\(Y_{i}^{(1)}\)</span> <span class="math inline">\(Y_{i}^{(0)}\)</span>. This is known as <strong>the fundamental problem of causal inference</strong>.</p>
</section>
<section class="level2" data-number="2.2" id="identification-of-the-ate">
<h2 class="anchored" data-anchor-id="identification-of-the-ate" data-number="2.2"> Identification of the ATE</h2>
<p>Although we cannot compute the individual treatment effect, we can estimate the Average Treatment Effect (ATE), which is the average causal effect of the treatment on the population using randomization.</p>
<p>Assume we observe <span class="math inline">\(n\)</span> individuals, indexed by <span class="math inline">\(i \in \mathcal{I}\)</span>. For each unit <span class="math inline">\(i\)</span>, and for each treatment level there are corresponding potential outcomes <span class="math inline">\(Y_i^{(0)}\)</span> and <span class="math inline">\(Y_i^{(1)}\)</span>. For <span class="math inline">\(t \in \{0, 1\}\)</span>, we define the random variables <span class="math inline">\(Y^{(t)}\)</span> and <span class="math inline">\(T\)</span> that associate to <span class="math inline">\(i \in \mathcal{I}\)</span> respectively <span class="math inline">\(Y_i^{(t)}\)</span> and <span class="math inline">\(T_i\)</span>.</p>
<div class="Definition" id="ATE" title="Average Treatment Effect (ATE)">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 2.1: </strong>Average Treatment Effect (ATE)</summary><div>We define the Average Treatment Effect as: <span class="math display">\[\tau = \mathbb{E}\left[Y^{(1)} - Y^{(0)}\right]\]</span><p></p>
</div></details>
</div>
<p><span class="math inline">\(\mathbb{E}[Y^{(t)}]\)</span> cannot be estimated by computing <span class="math inline">\(\mathbb{E}[Y^{(\text{\tiny obs})}|T=t]\)</span> which is the mean of <span class="math inline">\(Y^{(\text{\tiny obs})}\)</span> for the sub-population that received treatment <span class="math inline">\(t\)</span> because in general the sub-population that received treatment <span class="math inline">\(T=t\)</span> is different (for instance older people, sick people…) from the population that did not. <strong>To properly measure the causal eﬀect, two similar groups of people are needed</strong>. Hence <span class="math inline">\(\mathbb{E}[Y^{(t)}]\)</span> is the expectancy of <span class="math inline">\(Y^{(\text{\tiny obs})}\)</span> had everybody received treatment <span class="math inline">\(T=t\)</span>. This is often denoted with the <span class="math inline">\(do\)</span> operator as <span class="math inline">\(\mathbb{E}[Y^{(\text{\tiny obs})} | do(T=t)]\)</span>. Note that this operator is interventional and offers to see the ATE as the expected difference of outcome had everybody received and not received the treatment. Since again due to the fundamental problem of causal inference we cannot observe both <span class="math inline">\(Y_i^{(0)}\)</span> and <span class="math inline">\(Y_i^{(1)}\)</span>. We need to build similar groups of people.</p>
</section>

</div>
