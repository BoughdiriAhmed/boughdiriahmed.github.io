---
layout: post
title: "Chapter 4 — RCT Estimators"
date: 2023-10-04
excerpt: "Horvitz-Thomson, Hajek, regression-based and doubly-robust estimators for the ATE in RCTs, with finite-sample and asymptotic analyses."
---

<div class="course-chapter">
<p class="chapter-nav">
  Course: <a href="/blog/">Finite Sample and Asymptotic Estimators in Causal Inference</a>
</p>

<p>Now that we have defiend the framework and the assumptions under which we are working. We can build estimators of the average treatment effect.</p>
<section class="level2" data-number="4.1" id="horvitz-thomson-estimator">
<h2 class="anchored" data-anchor-id="horvitz-thomson-estimator" data-number="4.1"> Horvitz-Thomson estimator</h2>
<div class="Definition" id="horvitz-thomson-estimator-1" title="Horvitz-Thomson estimator">
<details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 4.1: </strong>Horvitz-Thomson estimator</summary><div>
<p>The Horvitz-Thomson estimator is denoted <span class="math inline">\(\hat{\tau}_{HT,n}\)</span> and defined as, <span class="math display">\[\hat{\tau}_{HT,n} = \frac{1}{n}\sum_{i=1}^n \left( \frac{T_iY_i}{e} - \frac{(1-T_i)Y_i}{1-e} \right) \]</span> where <span class="math inline">\(e\)</span> is:</p>
<ul>
<li>the probability of having the treatment under a Bernoulli trial</li>
<li>the proportion of treated under a Completely randomized trial</li>
</ul>
</div></details>
</div>
<p>This estimator was introduced by Daniel G. Horvitz and Donovan J. Thompson in 1952. They used inverse probability weighting (which is a recurrent technic used in estimators) is applied to account for different proportions of observations within strata in a target population.</p>
<div class="Proposition" id="unbiasedness-consistancy-of-hattau_htn-in-a-bernoulli-trial" title="Unbiasedness consistancy of \hat{\tau}_{HT,n} in a Bernoulli trial">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 4.1: </strong>Unbiasedness consistancy of <span class="math inline">\(\hat{\tau}_{HT,n}\)</span> in a Bernoulli trial</summary><div>Under a Bernoulli trial we have : <span class="math display">\[\mathbb{E}_{\mathcal{B}}[\hat{\tau}_{HT,n}]=\tau\]</span> and its variance satisfies, for all n, <span class="math display">\[n \mathbb{Var}_{\mathcal{B}}[\hat{\tau}_{HT,n}] =  \mathbb{E}\left[ \frac{(Y^{(1)})^2}{\pi}\right] + \mathbb{E}\left[ \frac{(Y^{(0)})^2}{1-\pi}\right] - \tau^2 := V_{HT} \]</span><p></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-4.1">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div><strong>Bias</strong> <span class="math display">\[\begin{align*}
    \mathbb{E}_{\mathcal{B}}[\hat{\tau}_{HT,n}] &amp;= \frac{\mathbb{E}_{\mathcal{B}}[TY^{(1)}]}{e} - \frac{\mathbb{E}_{\mathcal{B}}[(1-T)Y^{(0)}]}{1-e} &amp;&amp; \text{Linearity, I.I.D and SUTVA} \\
    &amp;= \frac{\mathbb{E}_{\mathcal{B}}[T]\mathbb{E}_{\mathcal{B}}[Y^{(1)}]}{e} - \frac{\mathbb{E}_{\mathcal{B}}[(1-T)]\mathbb{E}_{\mathcal{B}}[Y^{(0)}]}{1-e} &amp;&amp; \text{Randomization} \\
    &amp;= \frac{\pi \mathbb{E}_{\mathcal{B}}[Y^{(1)}]}{e} - \frac{(1-\pi)\mathbb{E}_{\mathcal{B}}[Y^{(0)}]}{1-e} &amp;&amp; \text{Def of $\pi$ in Bernoulli design} \\
    &amp;= \tau &amp;&amp; \text{e := $\pi$ in Bernoulli design}
\end{align*}\]</span><p></p>
<p><strong>Variance</strong> <span class="math display">\[\begin{align*}
    \mathbb{Var}_{\mathcal{B}}[\hat{\tau}_{HT,n}] &amp;= \mathbb{Var}_{\mathcal{B}}\left[\frac{1}{n}\sum_{i=1}^n  \frac{T_iY_i}{e} - \frac{(1-T_i)Y_i}{1-e}\right] \\
    &amp;=\frac{1}{n^2} \mathbb{Var}_{\mathcal{B}}\left[\sum_{i=1}^n  \frac{T_iY^{(1)}_i}{e} - \frac{(1-T_i)Y^{(0)}_i}{1-e}\right]  &amp;&amp; \text{SUTVA} \\
    &amp;= \frac{1}{n} \mathbb{Var}_{\mathcal{B}}\left[\frac{TY^{(1)}}{e} - \frac{(1-T)Y^{(0)}}{1-e}\right]  &amp;&amp; \text{I.I.D}
\end{align*}\]</span> Then, <span class="math display">\[\mathbb{Var}_{\mathcal{B}}[\hat{\tau}_{HT,n}] = \frac{1}{n}\left(\mathbb{Var}_{\mathcal{B}}\left[\frac{TY^{(1)}}{e}\right] + \mathbb{Var}_{\mathcal{B}}\left[\frac{(1-T)Y^{(0)}}{1-e}\right] -2\text{Cov}_{\mathcal{B}}\left[\frac{TY^{(1)}}{e}, \frac{(1-T)Y^{(0)}}{1-e}\right]\right)\]</span> The first two terms can be simplified, noting that <span class="math display">\[\begin{align*}
    \mathbb{E}_{\mathcal{B}}\left[\left(\frac{TY^{(1)}}{e}\right)^2\right] &amp;= \mathbb{E}_{\mathcal{B}}\left[\mathbb{1}_{T=1}\left(\frac{Y^{(1)}}{e}\right)^2\right] &amp;&amp; \text{A is binary} \\
    &amp;= \mathbb{E}_{\mathcal{B}}\left[\left(\frac{Y^{(1)}}{e}\right)^2\right] \mathbb{E}_{\mathcal{B}}\left[\mathbb{1}_{T=1}\right]  &amp;&amp; \text{Randomization of trial} \\
    &amp;= \mathbb{E}_{\mathcal{B}}\left[\frac{(Y^{(1)})^2}{e}\right]   &amp;&amp; \text{Definition of $e$}
\end{align*}\]</span> Similarly, <span class="math display">\[\mathbb{E}_{\mathcal{B}}\left[\left(\frac{(1-T)Y^{(0)}}{1-e}\right)^2\right] = \mathbb{E}_{\mathcal{B}}\left[\frac{(Y^{(0)})^2}{1-e}\right]\]</span> So, <span class="math display">\[\begin{align*}
    \mathbb{Var}_{\mathcal{B}}\left[\frac{TY^{(1)}}{e}\right] &amp;= \mathbb{E}_{\mathcal{B}}\left[\left(\frac{TY^{(1)}}{e}\right)^2\right] -\mathbb{E}_{\mathcal{B}}\left[\frac{TY^{(1)}}{e}\right]^2 \\
    &amp;= \mathbb{E}_{\mathcal{B}}\left[\frac{(Y^{(1)})^2}{e}\right] -  \mathbb{E}_{\mathcal{B}}\left[Y^{(1)}\right]^2
\end{align*}\]</span> Similarly, <span class="math display">\[\mathbb{Var}_{\mathcal{B}}\left[\frac{(1-T)Y^{(0)}}{e}\right] = \mathbb{E}_{\mathcal{B}}\left[\frac{(Y^{(0)})^2}{1-e}\right] -  \mathbb{E}_{\mathcal{B}}\left[Y^{(0)}\right]^2 \]</span> The third covariance term can also be decomposed, so that, <span class="math display">\[\begin{align*}
    \text{Cov}_{\mathcal{B}}\left[\frac{TY^{(1)}}{e}, \frac{(1-T)Y^{(0)}}{1-e}\right] &amp;= \mathbb{E}_{\mathcal{B}}\left[\left(\frac{TY^{(1)}}{e}- \mathbb{E}_{\mathcal{B}}[Y^{(1)}]\right)\left(\frac{(1-T)Y^{(0)}}{1-e}- \mathbb{E}_{\mathcal{B}}[Y^{(0)}]\right)\right] \\
    &amp;= \mathbb{E}_{\mathcal{B}}\left[\underbrace{\frac{TY^{(1)}}{e}\frac{(1-T)Y^{(0)}}{1-e}}_{=0}\right]-\mathbb{E}_{\mathcal{B}}[Y^{(1)}]\mathbb{E}_{\mathcal{B}}[Y^{(0)}]
\end{align*}\]</span> Finally, <span class="math display">\[n \mathbb{Var}_{\mathcal{B}}[\hat{\tau}_{HT,n}] =  \mathbb{E}\left[ \frac{(Y^{(1)})^2}{\pi}\right] + \mathbb{E}\left[ \frac{(Y^{(0)})^2}{1-\pi}\right] - \tau^2 := V_{HT} \]</span></p>
</div></details>
</div>
<div class="Proposition" id="unbiased-consistancy-of-hattau_htn-in-a-completely-randomized-trial" title="Unbiased consistancy of \hat{\tau}_{HT,n} in a Completely randomized trial">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 4.2: </strong>Unbiased consistancy of <span class="math inline">\(\hat{\tau}_{HT,n}\)</span> in a Completely randomized trial</summary><div>Under a Completely randomized trial we have : <span class="math display">\[\mathbb{E}_{\mathcal{C}}[\hat{\tau}_{HT,n}]=\tau\]</span> and its variance satisfies, for all n, <span class="math display">\[\mathbb{Var}_{\mathcal{C}}[\hat{\tau}_{HT,n}] =  \frac{\mathbb{Var}\left[Y^{(1)}\right]}{n_1} + \frac{\mathbb{Var}\left[Y^{(0)}\right]}{n_0}\]</span><p></p>
<p>where <span class="math inline">\(n_1= \sum_{i=1}^n T_i\)</span> and <span class="math inline">\(n_0= \sum_{i=1}^n 1- T_i\)</span></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-4.2">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div><strong>Bias</strong> <span class="math display">\[\begin{align*}
    \mathbb{E}_{\mathcal{C}}[\hat{\tau}_{HT,n}] &amp;= \sum_{i=1}^n\frac{\mathbb{E}_{\mathcal{C}}[T_iY^{(1)}_i]}{e} - \frac{\mathbb{E}_{\mathcal{C}}[(1-T_i)Y^{(0)}_i]}{1-e} &amp;&amp; \text{Linearity and SUTVA} \\
    &amp;= \sum_{i=1}^n\frac{\mathbb{E}_{\mathcal{C}}[T_i]\mathbb{E}_{\mathcal{C}}[Y^{(1)}_i]}{e} - \frac{\mathbb{E}_{\mathcal{C}}[(1-T_i)]\mathbb{E}_{\mathcal{C}}[Y^{(0)}_i]}{1-e} &amp;&amp; \text{Randomization} \\
    &amp;= \sum_{i=1}^n\frac{\frac{n_1}{n} \mathbb{E}_{\mathcal{C}}[Y^{(1)}_i]}{\frac{n_1}{n}} - \frac{(1-\frac{n_1}{n})\mathbb{E}_{\mathcal{C}}[Y^{(0)}_i]}{1-\frac{n_1}{n}} &amp;&amp; \text{Def of $e$ in Bernoulli design} \\
    &amp;= \frac{\frac{n_1}{n} \mathbb{E}_{\mathcal{C}}[Y^{(1)}]}{\frac{n_1}{n}} - \frac{(1-\frac{n_1}{n})\mathbb{E}_{\mathcal{C}}[Y^{(0)}]}{1-\frac{n_1}{n}} &amp;&amp; \text{I.I.D of $Y^{(1)}_i$ and $Y^{(0)}_i$} \\
    &amp;= \tau &amp;&amp; \text{Linearity}
\end{align*}\]</span> <strong>Variance</strong><p></p>
<p>Using the law of total variance, and conditioning on the treatment assignment vector <span class="math inline">\(T\)</span>, one has <span class="math display">\[\begin{align*}
    \mathbb{Var}_{\mathcal{C}}\left[\hat{\tau}_{HT,n}\right] &amp;= \mathbb{E}_{\mathcal{C}}\left[\mathbb{Var}_{\mathcal{C}}\left[\hat{\tau}_{HT,n}|T\right]\right] + \mathbb{Var}_{\mathcal{C}}\left[\mathbb{E}_{\mathcal{C}}\left[\hat{\tau}_{HT,n}|T\right]\right]
\end{align*}\]</span> We first start with the second term of the equation: <span class="math display">\[\begin{align*}
    \mathbb{E}_{\mathcal{C}}\left[\hat{\tau}_{HT,n}|T\right] &amp;= \frac{1}{n}\sum_{i=1}^n\mathbb{E}_{\mathcal{C}}\left[\frac{T_iY_i^{(1)}}{e} - \frac{(1-T_i)Y_i^{(0)}}{1-e}|T\right] &amp;&amp; \text{Using linearity and Consistency} \\
    &amp;= \frac{1}{n} \sum_{i=1}^n \frac{T_i}{e} \mathbb{E}_{\mathcal{C}}\left[Y_i^{(1)}|T\right] - \frac{(1-T_i)}{1-e} \mathbb{E}_{\mathcal{C}}\left[Y_i^{(0)}|T\right] &amp;&amp; \text{$T_i$ is measurable with respect to T}\\
    &amp;= \frac{1}{n}\sum_{i=1}^n\frac{T_i}{e}\mathbb{E}_{\mathcal{C}}\left[Y_i^{(1)}\right] - \frac{(1-T_i)}{1-e}\mathbb{E}_{\mathcal{C}}\left[Y_i^{(0)}\right] &amp;&amp; \text{Exchangeability}\\
    &amp;= \left(\frac{1}{n}\sum_{i=1}^n T_i \right)  \frac{\mathbb{E}\left[Y_i^{(1)}\right]}{e} - \left(\frac{1}{n}\sum_{i=1}^n 1-T_i \right) \frac{\mathbb{E}\left[Y_i^{(0)}\right]}{1-e} &amp;&amp; \text{the expectation of  $Y$ is independent of design} \\
    &amp;= \left(\frac{n1 }{n} \right)  \frac{\mathbb{E}\left[Y_i^{(1)}\right]}{\frac{n_1}{n}} - \left(\frac{n-n_1}{n}\right) \frac{\mathbb{E}\left[Y_i^{(0)}\right]}{\frac{n-n_1}{n}} &amp;&amp; \text{def. of e in Completely randomized trial} \\
    &amp;= \tau \\
\end{align*}\]</span> Therefore, we have that <span class="math inline">\(\mathbb{Var}_{\mathcal{C}}\left[\mathbb{E}_{\mathcal{C}}\left[\hat{\tau}_{HT,n}|T\right]\right] = 0\)</span> since <span class="math inline">\(\tau\)</span> is constant.</p>
<p>Now, we look at the first term:</p>
<p><span class="math display">\[\begin{align*}
\mathbb{Var}_{\mathcal{C}}\left[\hat{\tau}_{HT,n}|T\right] &amp;= \frac{1}{n^2} \mathbb{Var}_{\mathcal{C}}\left[\sum_{i=1}^n \frac{T_iY_i^{(1)}}{e} - \frac{(1-T_i)Y_i^{(0)}}{1-e}|T\right] &amp;&amp;\text{Consistency}\\
&amp;= \frac{1}{n^2} \left( \mathbb{Var}_{\mathcal{C}}\left[\sum_{i=1}^n \frac{T_iY_i^{(1)}}{e}|T\right] + \mathbb{Var}_{\mathcal{C}}\left[\sum_{i=1}^n \frac{(1-T_i)Y_i^{(0)}}{1-e}|T\right] \right)  \\
&amp;+ \frac{2}{n^2} \mathbb{Cov}_{\mathcal{C}}\left[\sum_{i=1}^n \frac{T_iY_i^{(1)}}{e} ; \sum_{j=1}^n\frac{(1-T_j)Y_j^{(0)}}{1-e}|T\right]
\end{align*}\]</span></p>
<p>We first focus on the first term:</p>
<p><span class="math display">\[\begin{align*}
\mathbb{Var}_{\mathcal{C}}\left[\sum_{i=1}^n \frac{T_iY_i^{(1)}}{e}|T\right] &amp;= \mathbb{Var}_{\mathcal{C}}\left[\sum_{T_i=1} \frac{Y_i^{(1)}}{e}|T\right] \\
&amp;= \mathbb{Var}_{\mathcal{C}}\left[\sum_{i=1}^{n_1} \frac{Y_i^{(1)}}{e}|T\right] &amp;&amp;\text{Since $ Y_i $  are i.i.d and are independant from $ T_i $}\\
&amp;= \mathbb{Var}_{\mathcal{C}}\left[\sum_{i=1}^{n_1} \frac{Y_i^{(1)}}{e}|n_1\right] \\
&amp;= \frac{n_1}{e^2} \mathbb{Var}[Y_i^{(1)}]
\end{align*}\]</span></p>
<p>Similarly, we also have:</p>
<p><span class="math display">\[\begin{align*}
\mathbb{Var}_{\mathcal{C}}\left[\sum_{i=1}^n \frac{(1-T_i)Y_i^{(0)}}{1-e}|T\right] = \frac{n_0}{(1-e-)^2} \mathbb{Var}[Y_i^{(0)}]
\end{align*}\]</span></p>
<p>and for the third term we have:</p>
<p><span class="math display">\[\begin{align*}
\mathbb{Cov}_{\mathcal{C}}\left[\sum_{i=1}^n \frac{T_iY_i^{(1)}}{e} ; \sum_{j=1}^n\frac{(1-T_j)Y_j^{(0)}}{1-e}|T\right] &amp;= \sum_{i=1}^n \sum_{j=1}^n \frac{T_i(1-T_j)}{e(1-e)}  \mathbb{Cov}_{\mathcal{C}}\left[ Y_i; Y_j|T\right] &amp;&amp; \text{linearity and Consistency}\\
&amp;= \sum_{i=1}^n \sum_{j=1}^n \frac{T_i(1-T_j)}{e(1-e)}  \mathbb{Cov}_{\mathcal{C}}\left[ Y_i; Y_j\right] &amp;&amp; \text{$Y_i$ are independent from $T$}\\
&amp;= \sum_{i=1}^n \sum_{j=1}^n \frac{T_i(1-T_j)}{e(1-e)} \delta_{ij} \mathbb{Var}(Y_i) &amp;&amp; \text{$Y_i$ are independent}\\
&amp;= 0
\end{align*}\]</span></p>
<p>Therefore we have that,</p>
<p><span class="math display">\[\begin{align*}
\mathbb{E}_{\mathcal{C}}\left[\mathbb{Var}_{\mathcal{C}}\left[\hat{\tau}_{HT,n}|T\right]\right] &amp;= \mathbb{E}_{\mathcal{C}}\left[\frac{1}{n^2} \left(\frac{n_1}{e^2} \mathbb{Var}[Y_i^{(1)}] +  \frac{n_0}{(1-e)^2} \mathbb{Var}[Y_i^{(0)}]\right)\right]\\
&amp;=  \frac{\mathbb{Var}\left[Y^{(1)}\right]}{n_1} + \frac{\mathbb{Var}\left[Y^{(0)}\right]}{n_0}
\end{align*}\]</span></p>
</div></details>
</div>
</section>
<section class="level2" data-number="4.2" id="difference-in-means---neyman-estimator">
<h2 class="anchored" data-anchor-id="difference-in-means---neyman-estimator" data-number="4.2"> Difference-in-means - Neyman estimator</h2>
<div class="Definition" id="difference-in-means---neyman-estimator-1" title="Difference-in-means - Neyman estimator">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 4.2: </strong>Difference-in-means - Neyman estimator</summary><div>The Difference-in-means or Neyman estimator is denoted <span class="math inline">\(\hat{\tau}_{HT,n}\)</span> and defined as, <span class="math display">\[\hat{\tau}_{DM,n} = \frac{1}{n_1}\sum_{T_i=1}Y_i -\frac{1}{n_0}\sum_{T_i=0}Y_i\]</span><p></p>
</div></details>
</div>
<p>The Difference-in-Means estimator can be viewed as a variant of the Horvitz-Thomson estimator, where the probability to be treated <span class="math inline">\(e\)</span> (or propensity score) is estimated, that is,</p>
<p><span class="math display">\[\hat{\tau}_{DM,n} = \frac{1}{n} \sum_{i=1}^n \left( \frac{T_iY_i}{\hat{e}} - \frac{(1-T_i)Y_i}{1-\hat{e}} \right) \]</span></p>
<p>where <span class="math inline">\(\hat{e} = \frac{1}{n}\sum_{i=1}^n T_i\)</span>.</p>
<div class="Proposition" id="asymptotically-unbiasedness-consistancy-of-hattau_dmn-under-a-bernoulli-design" title="Asymptotically unbiasedness consistancy of \hat{\tau}_{DM,n} under a Bernoulli design">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 4.3: </strong>Asymptotically unbiasedness consistancy of <span class="math inline">\(\hat{\tau}_{DM,n}\)</span> under a Bernoulli design</summary><div>Under a Bernoulli design we have for all n, <span class="math display">\[ \mathbb{E}_{\mathcal{B}}[\hat{\tau}_{DM,n}]=\tau + \pi^n \mathbb{E}[Y_i^{(0)}] - (1-\pi)^n \mathbb{E}[Y_i^{(1)}] \]</span> <span class="math display">\[n \mathbb{Var}_{\mathcal{B}}[\hat{\tau}_{DM,n}] = \mathbb{E}_{\mathcal{B}}\left[\frac{\mathbb{1}_{\hat{e}&gt;0}}{\hat{e}}\right]\mathbb{Var}[Y^{(1)}] + \mathbb{E}_{\mathcal{B}}\left[\frac{\mathbb{1}_{1-\hat{e}&gt;0}}{1-\hat{e}}\right]\mathbb{Var}[Y^{(0)}] + \mathcal{O}(\max{(\pi, 1-\pi)}^n)\]</span> Asymptotically, the difference-in-means estimator is unbiased: <span class="math display">\[\mathbb{E}_{\mathcal{B}}[\hat{\tau}_{DM,n}]=\tau \]</span> and its large sample variance satisfies, <span class="math display">\[\lim_{n\to \infty} n \mathbb{Var}_{\mathcal{B}}[\hat{\tau}_{DM,n}] = \frac{\mathbb{Var}[Y^{(1)}]}{\pi} + \frac{\mathbb{Var}[Y^{(0)}]}{1-\pi} := V_{DM, \infty}\]</span><p></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-4.3">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div><strong>Bias</strong><p></p>
<p>One can use the law of total expectation, conditioning on the treatment assignment vector denoted <span class="math inline">\(\mathbf{T}\)</span>, <span class="math display">\[\begin{align*}
    \mathbb{E}_{\mathcal{B}}[\hat{\tau}_{DM,n}] &amp;= \mathbb{E}_{\mathcal{B}}[\mathbb{E}_{\mathcal{B}}[\hat{\tau}_{DM,n}|\mathbf{T}]]\\
    &amp;= \mathbb{E}_{\mathcal{B}}\left[\frac{\frac{1}{n}\sum_{i=1}^n{T_i}}{\frac{1}{n}\sum_{i=1}^n{T_i}}\mathbb{E}[Y_i^{(1)}|\mathbf{T}] - \frac{\frac{1}{n}\sum_{i=1}^n{(1-T_i)}}{\frac{1}{n}\sum_{i=1}^n{(1-T_i)}}\mathbb{E}[Y_i^{(0)}|\mathbf{T}]\right] \\
    &amp;=\mathbb{E}_{\mathcal{B}}\left[\frac{\frac{1}{n}\sum_{i=1}^n{T_i}}{\frac{1}{n}\sum_{i=1}^n{T_i}}\mathbb{E}[Y_i^{(1)}] - \frac{\frac{1}{n}\sum_{i=1}^n{(1-T_i)}}{\frac{1}{n}\sum_{i=1}^n{(1-T_i)}}\mathbb{E}[Y_i^{(0)}]\right]  &amp;&amp; \{Y_i^{(0)}, Y_i^{(1)}\} \perp\mkern-9.5mu\perp T_i \\
    &amp;= \mathbb{E}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n{T_i}&gt;0}\mathbb{E}[Y_i^{(1)}] - \mathbb{1}_{\sum_{i=1}^n{1-T_i}&gt;0}\mathbb{E}[Y_i^{(0)}]\right]\\
    &amp;= \mathbb{E}[Y_i^{(1)}] \mathbb{E}_{\mathcal{B}}[\mathbb{1}_{\sum_{i=1}^n{T_i}&gt;0}]  - \mathbb{E}[Y_i^{(0)}] \mathbb{E}_{\mathcal{B}}[\mathbb{1}_{\sum_{i=1}^n{(1-T_i)}&gt;0}] &amp;&amp; \{Y_i^{(0)}, Y_i^{(1)}\} \perp\mkern-9.5mu\perp T_i \\
    &amp;= \mathbb{E}[Y_i^{(1)}] (1-(1-\pi)^n)  - \mathbb{E}[Y_i^{(0)}] (1-(\pi)^n)\\
    &amp;= \tau - (1-\pi)^n\mathbb{E}[Y_i^{(1)}] + (\pi)^n\mathbb{E}[Y_i^{(0)}]
\end{align*}\]</span> where the second row uses linearity of expectation and the conditioning on <span class="math inline">\(\mathbf{T}\)</span>. To summarize, the difference- in-means has a finite sample bias, <span class="math display">\[\mathbb{E}_{\mathcal{B}}[\hat{\tau}_{DM,n}] = \tau - (1-\frac{n_1}{n})^n\mathbb{E}[Y_i^{(1)}] + (\frac{n_1}{n})^n\mathbb{E}[Y_i^{(0)}]\]</span></p>
<p><strong>Variance</strong></p>
<p>Using the law of total variance, and conditioning on the treatment assignment vector <span class="math inline">\(\mathbf{T}\)</span>, one has <span class="math display">\[\begin{align*}
    \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \right] &amp;=    \operatorname{Var}_{\mathcal{B}}\left[\mathbb{E}_{\mathcal{B}}\left[   \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T}\right] \right]  +   \mathbb{E}_{\mathcal{B}}\left[ \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T} \right] \right].
\end{align*}\]</span></p>
<p>Recall from derivations about the bias that,</p>
<p><span class="math display">\[\begin{align*}
     \mathbb{E}_{\mathcal{B}}\left[  \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T}\right] &amp;=  \mathbb{1}_{\sum_{i=1}^n T_i &gt; 0}  \mathbb{E}\left[  Y_i^{(1)}\right] -  \mathbb{1}_{\sum_{i=1}^n 1-T_i &gt; 0} \mathbb{E}_{\mathcal{B}}\left[  Y_i^{(0)}\right].
\end{align*}\]</span></p>
<p>Here, one has,</p>
<p><span class="math display">\[\begin{align*}
  \operatorname{Var}_{\mathcal{B}}\left[\mathbb{E}_{\mathcal{B}}\left[   \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T}\right] \right] &amp;=     \operatorname{Var}_{\mathcal{B}}\left[  \mathbb{1}_{\sum_{i=1}^n T_i &gt; 0}  \mathbb{E}\left[  Y_i^{(1)}\right] -  \mathbb{1}_{\sum_{i=1}^n 1-T_i &gt; 0} \mathbb{E}\left[  Y_i^{(0)}\right]  \right]\\
  &amp;=  \mathbb{E}\left[  Y_i^{(1)}\right]^2   \operatorname{Var}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n T_i &gt; 0}  \right] + \mathbb{E}\left[  Y_i^{(0)}\right]^2   \operatorname{Var}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n 1-T_i &gt; 0}  \right] \\
  &amp;\qquad -2   \mathbb{E}\left[  Y_i^{(1)}\right]  \mathbb{E}\left[  Y_i^{(0)}\right] \operatorname{Cov}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n T_i &gt; 0} , \mathbb{1}_{\sum_{i=1}^n 1-T_i &gt; 0}  \right].
\end{align*}\]</span></p>
<p>Besides,</p>
<p><span class="math display">\[\begin{align*}
      \operatorname{Var}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n T_i &gt; 0}  \right]  &amp;=  \mathbb{E}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n T_i &gt; 0} ^2 \right] -  \mathbb{E}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n T_i &gt; 0} \right]^2 \\
      &amp;= (1-\pi)^n\left( 1- (1-\pi)^n\right),
\end{align*}\]</span></p>
<p>and similarly,</p>
<p><span class="math display">\[\begin{align*}
          \operatorname{Var}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n 1-T_i &gt; 0}  \right]  &amp;=  \pi^n\left( 1- \pi^n\right).
\end{align*}\]</span></p>
<p>On the other hand,</p>
<p><span class="math display">\[\begin{align*}
    \operatorname{Cov}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n T_i &gt; 0} , \mathbb{1}_{\sum_{i=1}^n 1-T_i &gt; 0}  \right] &amp;= \mathbb{E}_{\mathcal{B}}\left[ \left(\mathbb{1}_{\sum_{i=1}^n T_i &gt; 0} - \left(1- (1-\pi)^n \right)  \right)  \left( \mathbb{1}_{\sum_{i=1}^n 1-T_i &gt; 0}- 1-\pi^n\right)  \right] \\
    &amp;= \mathbb{E}_{\mathcal{B}}\left[\mathbb{1}_{\sum_{i=1}^n T_i &gt; 0} \mathbb{1}_{\sum_{i=1}^n 1-T_i &gt; 0} \right] - \left(1- (1-\pi)^n \right)\left(1-\pi^n\right) \\
    &amp;= 1-(1-\pi)^n-\pi^n - \left(1- \pi^n - (1-\pi)^n - \pi^n(1-\pi)^n \right)\\
    &amp;=  \pi^n(1-\pi)^n,
\end{align*}\]</span></p>
<p>such that,</p>
<p><span class="math display">\[\begin{align*}
  \operatorname{Var}_{\mathcal{B}}\left[\mathbb{E}_{\mathcal{B}}\left[   \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T}\right] \right] &amp;=   \mathbb{E}\left[  Y_i^{(1)}\right]^2  (1-\pi)^n\left( 1- (1-\pi)^n\right)+  \mathbb{E}\left[  Y_i^{(0)}\right]^2  \pi^n\left( 1- \pi^n\right)-2 \mathbb{E}\left[  Y_i^{(1)}\right]  \mathbb{E}\left[  Y_i^{(0)}\right] \pi^n(1-\pi)^n \\
  &amp;=  \mathbb{E}\left[  Y_i^{(1)}\right]^2 (1-\pi)^n +  \mathbb{E}\left[  Y_i^{(0)}\right]^2  \pi^n - \left(\mathbb{E}\left[  Y_i^{(1)}\right] (1-\pi)^n  +  \mathbb{E}\left[  Y_i^{(0)}\right]  \pi^n \right)^2 \\
% &amp; \leq   (1-\pi)^n  \mathbb{E}\left[  Y_i^{(1)}\right]^2 + \pi^n  \mathbb{E}\left[  Y_i^{(0)}\right]^2-2\pi^n(1-\pi)^n \mathbb{E}\left[  Y_i^{(1)}\right] \mathbb{E}\left[  Y_i^{(0)}\right] \\
&amp; \leq \mathbb{E}\left[  Y_i^{(1)}\right]^2 (1-\pi)^n +  \mathbb{E}\left[  Y_i^{(0)}\right]^2  \pi^n \\
  &amp; \leq \left( \mathbb{E}\left[  Y^{(1)}\right]^2 + \mathbb{E}\left[  Y^{(0)}\right]^2\right) \max(\pi, 1 - \pi)^n.
\end{align*}\]</span></p>
<p>Now,</p>
<p><span class="math display">\[\begin{align*}
    \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T} \right]  &amp;=  \operatorname{Var}_{\mathcal{B}}\left[ \frac{1}{n}  \sum_{i=1}^n \left( \frac{T_i Y_i^{(1)}}{\hat \pi}  - \frac{(1-T_i)Y_i^{(0)}  }{1-\hat \pi} \right) \mid \mathbf{T} \right] \\
    &amp;= \frac{1}{n}  \operatorname{Var}_{\mathcal{B}}\left[   \frac{T_i Y_i^{(1)}}{\hat \pi}  - \frac{(1-T_i)Y_i^{(0)}  }{1-\hat \pi} \mid \mathbf{T} \right] &amp;&amp; \text{iid}\\
    &amp;=  \frac{1}{n}  \left(  \operatorname{Var}_{\mathcal{B}}\left[ \frac{T_i Y_i^{(1)}}{\hat \pi}  \mid \mathbf{T}\right] + \operatorname{Var}_{\mathcal{B}}\left[ \frac{(1-T_i)Y_i^{(0)}  }{1-\hat \pi}  \mid \mathbf{T}\right]  - 2 \operatorname{Cov}_{\mathcal{B}}\left[ \frac{T_i Y_i^{(1)}}{\hat \pi} , \frac{(1-T_i)Y_i^{(0)}  }{1-\hat \pi} \mid \mathbf{T} \right]\right).
\end{align*}\]</span></p>
<p>Now, developing the covariance term, it is possible to show that,</p>
<p><span class="math display">\[\begin{align*}
    \operatorname{Cov}_{\mathcal{B}}\left[ \frac{T_i Y_i^{(1)}}{\hat \pi} , \frac{(1-T_i)Y_i^{(0)}  }{1-\hat \pi} \mid \mathbf{T} \right] &amp;= - \mathbb{E}_{\mathcal{B}}\left[ \frac{(1-T_i)Y_i^{(0)}  }{1-\hat \pi} \mid \mathbf{T} \right] \mathbb{E}_{\mathcal{B}}\left[ \frac{T_iY_i^{(1)}  }{\hat \pi} \mid \mathbf{T} \right] \\
    &amp;=  -  \frac{(1-T_i)\mathbb{E}_{\mathcal{B}}\left[Y_i^{(0)}  \mid \mathbf{T} \right] }{1-\hat \pi} \frac{T_i\mathbb{E}_{\mathcal{B}}\left[ Y_i^{(1)}  \mid \mathbf{T} \right] }{\hat \pi} &amp;&amp; \text{Linearity and conditioned on $\mathbf{T}$} \\
    &amp;= 0. &amp;&amp; \text{$T_i(1-T_i)=0$}
\end{align*}\]</span></p>
<p>Now, also using linearity of expectation, and the fact that we conditioned on <span class="math inline">\(\mathbf{T}\)</span>, one has</p>
<p><span class="math display">\[\begin{align*}
    \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T} \right]  &amp;=  \frac{1}{n}  \left(  \left( \frac{T_i}{\hat \pi}\right)^2 \operatorname{Var}_{\mathcal{B}}\left[Y_i^{(1)} \mid \mathbf{T}\right]   +  \left( \frac{1-T_i}{1- \hat \pi}\right)^2 \operatorname{Var}_{\mathcal{B}}\left[Y_i^{(0)} \mid \mathbf{T}\right]  \right) \\
     &amp;=  \frac{1}{n}  \left(  \left( \frac{T_i}{\hat \pi}\right)^2 \operatorname{Var}\left[Y_i^{(1)}\right]   +  \left( \frac{1-T_i}{1- \hat \pi}\right)^2 \operatorname{Var}\left[Y_i^{(0)}\right]  \right), &amp;&amp; \text{using $\{Y_i^{(1)}, Y_i^{(0)} \} \perp\mkern-9.5mu\perp  T_i $.}
\end{align*}\]</span></p>
<p>Taking the expecation of the previous term leads to,</p>
<p><span class="math display">\[\begin{align*}
     \mathbb{E}_{\mathcal{B}}\left[ \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T} \right] \right]&amp;= \mathbb{E}\left[ \frac{1}{n}  \left(  \left( \frac{T_i}{\hat \pi}\right)^2 \operatorname{Var}\left[Y_i^{(1)}\right]   +  \left( \frac{1-T_i}{1- \hat \pi}\right)^2 \operatorname{Var}\left[Y_i^{(0)}\right]  \right)\right] \\
     &amp;=  \frac{1}{n} \left(\mathbb{E}\left[ \left( \frac{T_i}{\hat \pi}\right)^2\right]  \operatorname{Var}\left[Y_i^{(1)}\right] + \frac{1}{n} \mathbb{E}\left[ \left( \frac{1-T_i}{1-\hat \pi}\right)^2\right]  \operatorname{Var}\left[Y_i^{(0)}\right] \right), &amp;&amp; \text{by linearity.}
\end{align*}\]</span></p>
<p>Note that,</p>
<p><span class="math display">\[\begin{align*}
     \mathbb{E}_{\mathcal{B}}\left[ \left( \frac{T_i}{\hat \pi}\right)^2\right]  &amp;=   \mathbb{E}_{\mathcal{B}}\left[  \frac{T_i}{\left(\hat \pi\right)^2}\right] \\
     &amp;= \frac{1}{n}\left(  \mathbb{E}_{\mathcal{B}}\left[  \frac{T_1}{\hat \pi^2}\right] +  \mathbb{E}_{\mathcal{B}}\left[  \frac{T_2}{\hat \pi^2}\right]  + \dots +  \mathbb{E}_{\mathcal{B}}\left[  \frac{T_n}{\hat \pi^2}\right] \right) \\
     &amp;= \mathbb{E}_{\mathcal{B}}\left[  \frac{\hat \pi}{\hat \pi^2}\right] \\
     &amp;= \mathbb{E}_{\mathcal{B}}\left[  \frac{\mathbb{1}_{\hat \pi &gt; 0} }{\hat \pi}\right],
\end{align*}\]</span></p>
<p>so that</p>
<p><span class="math display">\[\begin{align*}
         \mathbb{E}_{\mathcal{B}}\left[ \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T} \right] \right] &amp;=  \frac{1}{n} \left( \mathbb{E}_{\mathcal{B}}\left[  \frac{\mathbb{1}_{\hat \pi &gt; 0} }{\hat \pi}\right] \operatorname{Var}\left[Y_i^{(1)}\right] +  \mathbb{E}_{\mathcal{B}}\left[  \frac{\mathbb{1}_{(1-\hat \pi) &gt; 0} }{1-\hat \pi}\right]  \operatorname{Var}\left[Y_i^{(0)}\right] \right).
\end{align*}\]</span></p>
<p>Coming back to the law of total variance, one has,</p>
<p><span class="math display">\[\begin{align*}
     \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \right] &amp;=    \operatorname{Var}_{\mathcal{B}}\left[\mathbb{E}_{\mathcal{B}}\left[   \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T}\right] \right]  +   \mathbb{E}_{\mathcal{B}}\left[ \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \mid \mathbf{T} \right] \right] \\
     &amp;= \mathbb{E}\left[  Y_i^{(1)}\right]^2 (1-\pi)^n +  \mathbb{E}\left[  Y_i^{(0)}\right]^2  \pi^n - \left(\mathbb{E}\left[  Y_i^{(1)}\right] (1-\pi)^n  +  \mathbb{E}\left[  Y_i^{(0)}\right]  \pi^n \right)^2  \\
     &amp; \qquad + \frac{1}{n} \left( \mathbb{E}_{\mathcal{B}}\left[  \frac{\mathbb{1}_{\hat \pi &gt; 0} }{\hat \pi}\right] \operatorname{Var}\left[Y_i^{(1)}\right] +  \mathbb{E}_{\mathcal{B}}\left[  \frac{\mathbb{1}_{(1-\hat \pi) &gt; 0} }{1-\hat \pi}\right]  \operatorname{Var}\left[Y_i^{(0)}\right] \right)
\end{align*}\]</span></p>
<p>In particular, for any sample size,</p>
<p><span class="math display">\[\begin{align*}
      \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \right] &amp;= \frac{1}{n} \left( \mathbb{E}_{\mathcal{B}}\left[  \frac{\mathbb{1}_{\hat \pi &gt; 0} }{\hat \pi}\right] \operatorname{Var}\left[Y_i^{(1)}\right] +  \mathbb{E}_{\mathcal{B}}\left[  \frac{\mathbb{1}_{(1-\hat \pi) &gt; 0} }{1-\hat \pi}\right]  \operatorname{Var}\left[Y_i^{(0)}\right] \right) + \mathcal{O}\left(\max(\pi, 1-\pi)^n \right),
\end{align*}\]</span></p>
<p>and more particularly, <span class="math display">\[\begin{align*}
     \lim_{n\to\infty}  n \operatorname{Var}_{\mathcal{B}}\left[ \hat{\tau}_{\text{\tiny DM}} \right] &amp;= \frac{  \operatorname{Var}\left[ Y^{(1)}\right] }{\pi}+  \frac{  \operatorname{Var}\left[ Y^{(0)}\right] }{1-\pi}:=  V_{ \text{\tiny DM}, \infty}.
\end{align*}\]</span></p>
</div></details>
</div>
<div class="Proposition" id="asymptotically-unbiasedness-consistancy-of-hattau_dmn-under-a-completely-randomized-trial" title="Asymptotically unbiasedness consistancy of \hat{\tau}_{DM,n} under a Completely randomized trial">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 4.4: </strong>Asymptotically unbiasedness consistancy of <span class="math inline">\(\hat{\tau}_{DM,n}\)</span> under a Completely randomized trial</summary><div>Under a Completely randomized design we have for all n, <span class="math display">\[ \mathbb{E}_{\mathcal{C}}[\hat{\tau}_{DM,n}]=\tau \]</span> and its variance satisfies, for all n, <span class="math display">\[n \mathbb{Var}_{\mathcal{C}}[\hat{\tau}_{DM,n}] = \frac{\mathbb{Var}\left[Y^{(1)}\right]}{n_1} + \frac{\mathbb{Var}\left[Y^{(0)}\right]}{n_0}\]</span><p></p>
<p>where <span class="math inline">\(n_1= \sum_{i=1}^n T_i\)</span> and <span class="math inline">\(n_0= \sum_{i=1}^n 1- T_i\)</span></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-4.4">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div><strong>Bias</strong> <span class="math display">\[\begin{align*}
    \mathbb{E}_{\mathcal{C}}[\hat{\tau}_{DM,n}] &amp;= \frac{1}{n_1}\sum_{i=1}^n\mathbb{E}_{\mathcal{C}}[T_iY^{(1)}_i] - \frac{1}{n_0}\sum_{i=1}^n\mathbb{E}_{\mathcal{C}}[(1-T_i)Y^{(0)}_i] &amp;&amp; \text{Linearity and SUTVA} \\
    &amp;= \frac{1}{n_1}\sum_{i=1}^n\mathbb{E}_{\mathcal{C}}[T_i]\mathbb{E}_{\mathcal{C}}[Y^{(1)}_i] - \frac{1}{n_0}\sum_{i=1}^n\mathbb{E}_{\mathcal{C}}[(1-T_i)]\mathbb{E}_{\mathcal{C}}[Y^{(0)}_i] &amp;&amp; \text{Randomization} \\
    &amp;= \frac{1}{n_1}\sum_{i=1}^n \frac{n_1}{n}\mathbb{E}_{\mathcal{C}}[Y^{(1)}_i] - \frac{1}{n_0}\sum_{i=1}^n\frac{n_0}{n}\mathbb{E}_{\mathcal{C}}[Y^{(0)}_i] &amp;&amp; \text{Completely randomized trial} \\
    &amp;= \tau &amp;&amp; \text{Linearity}
\end{align*}\]</span><p></p>
<p><strong>Variance</strong></p>
<p>For the Proof of the variance we refer to the proof of Horvitz-Thomson under a Completely randomized trial since in this case Neyman is just a reformulation of Horvitz-Thomson.</p>
</div></details>
</div>
<p>Counter-intuitively, the benefit of estimating <span class="math inline">\(\pi\)</span> is to lower the variance. Even if the true probability is <span class="math inline">\(\pi = 0.5\)</span>, the actual treatment allocation in the sample can be different (e.g., <span class="math inline">\(\hat{\pi} = 0.48\)</span>), and using <span class="math inline">\(\hat{\pi}\)</span> rather than <span class="math inline">\(\pi\)</span> leads to a smaller large sample variance by adjusting to the exact observed probability to be treated in the trial. In particular, it is possible to be convinced of this phenomenon when comparing the two variances.</p>
<div class="Proposition" id="variance-inequality-between-a-hattau_htn-and-hattau_dmn-under-a-bernoulli-design" title="Variance inequality between a \hat{\tau}_{HT,n} and \hat{\tau}_{DM,n} under a Bernoulli design">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 4.5: </strong>Variance inequality between a <span class="math inline">\(\hat{\tau}_{HT,n}\)</span> and <span class="math inline">\(\hat{\tau}_{DM,n}\)</span> under a Bernoulli design</summary><div>Asymptotically under a Bernoulli design the variance of the difference-in-means estimator has a smaller variance than the Horvitz-Thomson estimator, <span class="math display">\[V_{DM, \infty} =  V_{HT} - \left( \sqrt{\frac{1-\pi}{\pi}} \mathbb{E}[Y^{(1)}] + \sqrt{\frac{\pi}{1-\pi}}\mathbb{E}[Y^{(0)}] \right)^2 \leq V_{HT}\]</span><p></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-4.5">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div>We have: <span class="math display">\[\begin{align*}
    V_{HT} &amp;= \mathbb{E}\left[ \frac{(Y^{(1)})^2}{\pi}\right] + \mathbb{E}\left[ \frac{(Y^{(0)})^2}{1-\pi}\right] - \tau^2 \\
    &amp;= \frac{1}{\pi} \left(\mathbb{Var}\left[Y^{(1)}\right] + \mathbb{E}\left[Y^{(1)}\right]^2\right) + \frac{1}{1-\pi} \left(\mathbb{Var}\left[(Y^{(0)})\right] + \mathbb{E}\left[Y^{(0)}\right]^2\right) - \tau^2 \\
    &amp;= V_{DM, \infty} + \frac{1}{\pi} \mathbb{E}\left[Y^{(1)}\right]^2 + \frac{1}{1-\pi}\mathbb{E}\left[(Y^{(0)})\right]^2 - \tau^2 \\
    &amp;= V_{DM, \infty} + \left( \frac{1}{\pi} - 1 \right)\mathbb{E}\left[Y^{(1)}\right]^2 + \left( \frac{1}{1-\pi} - 1 \right)\mathbb{E}\left[Y^{(0)}\right]^2 + 2\mathbb{E}\left[Y^{(0)}\right]\mathbb{E}\left[Y^{(1)}\right]\\
    &amp;= V_{DM, \infty} + \left( \sqrt{\frac{1-\pi}{\pi}} \mathbb{E}[Y^{(1)}] + \sqrt{\frac{\pi}{1-\pi}}\mathbb{E}[Y^{(0)}] \right)^2
\end{align*}\]</span><p></p>
</div></details>
</div>
<p>To conclude and summarize all of these properties we can build a table:</p>
<table class="table">
<colgroup>
<col style="width: 11%"/>
<col style="width: 7%"/>
<col style="width: 23%"/>
<col style="width: 57%"/>
</colgroup>
<thead>
<tr class="header">
<th></th>
<th></th>
<th>Horvitz-Thomson estimator</th>
<th>Difference-in-means - Neyman estimator</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Expectancy</strong></td>
<td><strong>Bernoulli</strong></td>
<td><span class="math inline">\(\tau\)</span></td>
<td><span class="math inline">\(\tau + \pi^n \mathbb{E}[Y_i^{(0)}] - (1-\pi)^n \mathbb{E}[Y_i^{(1)}]\)</span></td>
</tr>
<tr class="even">
<td></td>
<td><strong>C.randomized</strong></td>
<td><span class="math inline">\(\tau\)</span></td>
<td><span class="math inline">\(\tau\)</span></td>
</tr>
<tr class="odd">
<td><strong>Variance</strong></td>
<td><strong>Bernoulli</strong></td>
<td><span class="math inline">\(\frac{1}{n}\left(\mathbb{E}\left[ \frac{(Y^{(1)})^2}{\pi}\right] + \mathbb{E}\left[ \frac{(Y^{(0)})^2}{1-\pi}\right] - \tau^2\right)\)</span></td>
<td><span class="math inline">\(\frac{1}{n}\left( \mathbb{E}_{\mathcal{B}}\left[\frac{\mathbb{1}_{\hat{e}&gt;0}}{\hat{e}}\right]\mathbb{Var}[Y^{(1)}] + \mathbb{E}_{\mathcal{B}}\left[\frac{\mathbb{1}_{1-\hat{e}&gt;0}}{1-\hat{e}}\right]\mathbb{Var}[Y^{(0)}] + \mathcal{O}(\max{(\pi, 1-\pi)}^n)\right)\)</span></td>
</tr>
<tr class="even">
<td></td>
<td><strong>C.randomized</strong></td>
<td><span class="math inline">\(\frac{\mathbb{Var}_{\mathcal{C}}[Y^{(1)}]}{n_1} + \frac{\mathbb{Var}_{\mathcal{C}}[Y^{(0)}]}{n_0}\)</span></td>
<td><span class="math inline">\(\frac{\mathbb{Var}_{\mathcal{C}}[Y^{(1)}]}{n_1} + \frac{\mathbb{Var}_{\mathcal{C}}[Y^{(0)}]}{n_0}\)</span></td>
</tr>
</tbody>
</table>
</section>

</div>
