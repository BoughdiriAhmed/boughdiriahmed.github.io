---
layout: post
title: "Chapter 6 — Inverse Propensity Weighting"
date: 2023-10-06
excerpt: "Oracle and estimated IPW estimators, their asymptotic properties, and the role of propensity score estimation."
---

<div class="course-chapter">
<p class="chapter-nav">Course: <a href="/blog/">Finite Sample and Asymptotic Estimators in Causal Inference</a></p>

<p>A first way to understand the Inverse Propensity Weighting (IPW) is to understand what the oracle IPW. Let us say that we somehow found a way to predict perfectly $ x X()$ the propensity score <span class="math inline">\(e(x)\)</span>. Then we can define the Oracle Inverse Propensity Weighting estimator as:</p>
<div class="Definition" id="oracle-inverse-propensity-weighting-estimator" title="Oracle Inverse Propensity Weighting estimator">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 6.1: </strong>Oracle Inverse Propensity Weighting estimator</summary><div>Assume the propensity score <span class="math inline">\(e(X)\)</span> is a known function, then <span class="math inline">\(\hat{\tau}_{\text{\tiny IPW }}^{*}\)</span> denotes the oracle IPW estimator, <span class="math display">\[\begin{equation*}
    \hat{\tau}_{\text {\tiny IPW }}^{*}=\frac{1}{n} \sum_{i=1}^{n}\left(\frac{T_{i} Y_{i}}{e\left(X_{i}\right)}-\frac{\left(1-T_{i}\right) Y_{i}}{1-e\left(X_{i}\right)}\right)   .
\end{equation*}\]</span><p></p>
</div></details>
</div>
<div class="Proposition" id="oracle-ipw-unbiasedness" title="Oracle IPW unbiasedness">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 6.1: </strong>Oracle IPW unbiasedness</summary><div>The oracle IPW, denoted <span class="math inline">\(\hat{\tau}_{\text {\tiny IPW }}^{*}\)</span>, is an unbiased estimator of the average treatment effect <span class="math inline">\(\tau\)</span>, that is, <span class="math display">\[\begin{equation*}
    \mathbb{E}[\hat{\tau}_{\text{\tiny IPW }}^{*}] = \tau.
\end{equation*}\]</span><p></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-6.1">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div>Expectancy of the first term in the IPW gives, <span class="math display">\[\begin{align*}
    \mathbb{E}\left[ \frac{1}{n} \sum_{i=1}^{n}\left(\frac{T_{i} Y_{i}}{e\left(X_{i}\right)} \right)\right] &amp;= \frac{1}{n} \sum_{i=1}^{n}    \mathbb{E}\left[\frac{T_{i} Y_{i}}{e\left(X_{i}\right)} \right] &amp;&amp; \text{Linearity of $\mathbb{E}[.]$} \\
    &amp;=  \mathbb{E}\left[\frac{T_{i} Y_{i}^{(1)}}{e\left(X_{i}\right)} \right] &amp;&amp; \text{\textit{iid} and consistency} \\
    &amp;=  \mathbb{E}\left[ \mathbb{E}\left[\frac{T_{i} Y_{i}^{(1)}}{e\left(X_{i}\right)}  \mid X_i \right] \right] &amp;&amp; \text{Total probability}\\
    &amp;=  \mathbb{E}\left[ \frac{1}{e(X_i)}\mathbb{E}\left[T_{i} Y_{i}^{(1)} \mid X_i \right] \right] &amp;&amp; \text{$e(X)$ is a function of $X$}\\
        &amp;=  \mathbb{E}\left[ \frac{1}{e(X_i)}\mathbb{E}\left[Y_{i}^{(1)} \mid X_i \right] \mathbb{E}\left[T_{i}\mid X_i \right]  \right] &amp;&amp; \text{Uncounf.}\\
        &amp;=  \mathbb{E}\left[ \mathbb{E}\left[Y_{i}^{(1)} \mid X_i \right]  \right] &amp;&amp; \text{Def. of $e(X)$} \\
        &amp;= \mathbb{E}[Y_{i}^{(1)} ].
\end{align*}\]</span><p></p>
<p>Similarly one can show that,</p>
<p><span class="math display">\[\begin{equation*}
        \mathbb{E}\left[ \frac{1}{n} \sum_{i=1}^{n}\left(\frac{(1-T_{i}) Y_{i}}{1-e\left(X_{i}\right)} \right)\right] =  \mathbb{E}[Y_{i}^{(0)} ],
\end{equation*}\]</span></p>
<p>such that <span class="math inline">\(\mathbb{E}[\hat{\tau}_{\text {\tiny IPW }}^{*}] = \mathbb{E}[Y_{i}^{(1)}] - \mathbb{E}[Y_{i}^{(0)}] = \tau\)</span></p>
</div></details>
</div>
<p>In addition, the oracle IPW estimator is consistent with an asymptotic normality property.</p>
<div class="Proposition" id="consistency-and-asymptotic-normality-of-the-oracle-ipw-estimator" title="Consistency and asymptotic normality of the oracle IPW estimator">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 6.2: </strong>Consistency and asymptotic normality of the oracle IPW estimator</summary><div>The oracle IPW, denoted <span class="math inline">\(\hat{\tau}_{\text {\tiny IPW }}^{*}\)</span>, is consistent, <span class="math display">\[\hat{\tau}_{\text{\tiny IPW}}^* \stackrel{p}{\longrightarrow} \tau, \]</span><p></p>
<p>and is an asymptotically normal estimator, that is,</p>
<p><span class="math display">\[\sqrt{n}\left(\hat{\tau}_{\text{\tiny IPW}}^* - \tau \right) \stackrel{d}{\rightarrow} \mathcal{N}\left(0, V_{\text {\tiny IPW }^*}\right),\]</span></p>
<p>where, <span class="math display">\[V_{\text {\tiny IPW }}^{*} = \mathbb{E}\left[\frac{\left( Y^{(0)} \right)^2}{1-e(X)} + \frac{\left( Y^{(1)} \right)^2}{e(X)}\right]  - \tau^2.\]</span></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-6.2">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div><strong>Consistentcy:</strong> We have already showed that the oracle IPW is an unbiased estimator of <span class="math inline">\(\tau\)</span>. We can now calculate the variance of the oracle IPW:<p></p>
<p><span class="math display">\[\begin{align*}
V_{\text {\tiny IPW }}^* &amp;= \operatorname{Var}\left[ \frac{1}{n} \sum_{i=1}^{n}\left(\frac{T_{i} Y_{i}}{e\left(X_{i}\right)}-\frac{\left(1-T_{i}\right) Y_{i}}{1-e\left(X_{i}\right)}\right) \right] \\
&amp;= \frac{1}{n^2} \operatorname{Var}\left[ \sum_{i=1}^{n}\left(\frac{T_{i} Y_{i}}{e\left(X_{i}\right)}-\frac{\left(1-T_{i}\right) Y_{i}}{1-e\left(X_{i}\right)}\right) \right] &amp;&amp; \text{Variance property} \\
&amp;= \frac{1}{n} \operatorname{Var}\left[ \left(\frac{T Y}{e\left(X\right)}-\frac{\left(1-T\right) Y}{1-e\left(X\right)}\right) \right] &amp;&amp; \text{iid}  \\
&amp;= \frac{1}{n}  \mathbb{E}\left[  \left(\frac{(1-T) Y}{1-e(x)}-\mathbb{E}[Y^{(0)}]\right)^{2} + \left(\frac{T Y}{e(x)}-\mathbb{E}[Y^{(1)}]\right)^{2} \right] \\
&amp;\quad- \frac{2}{n} \mathbb{E}\left[ \left(\frac{(1-T) Y}{1-e(x)}-\mathbb{E}[Y^{(0)}]\right)\left(\frac{T Y}{e(x)}-\mathbb{E}[Y^{(1)}]\right) \right]   \\
&amp;= \frac{1}{n} \left( \mathbb{E}\left[ \left(\frac{(1-T) Y}{1-e(x)}\right)^{2} \right] -  \mathbb{E}[Y^{(0)}]^2  \right)+ \frac{1}{n} \left(\mathbb{E}\left[ \left(\frac{T Y}{e(x)}\right)^{2} \right] -  \mathbb{E}[Y^{(1)}]^2\right) \\
&amp; \quad \quad  - \frac{2}{n} \left(\underbrace{\mathbb{E}\left[ \frac{T (1-T) Y^2}{e(x)(1-e(x))}\right] }_{=0} -  \underbrace{\mathbb{E}[Y^{(1)}]\mathbb{E}\left[\frac{(1-T) Y}{1-e(x)}\right]-\mathbb{E}[Y^{(0)}]\mathbb{E}\left[\frac{T Y}{e(x)}\right] +\mathbb{E}[Y^{(1)}]\mathbb{E}[Y^{(0)}]}_{=\mathbb{E}[Y^{(1)}]\mathbb{E}[Y^{(0)}]} \right) \\
&amp;= \frac{1}{n} \left(\mathbb{E}\left[ \left(\frac{(1-T) Y}{1-e(x)}\right)^{2} \right] + \mathbb{E}\left[ \left(\frac{T Y}{e(x)}\right)^{2} \right] -  \mathbb{E}[Y^{(1)}]^2 - \mathbb{E}[Y^{(0)}]^2 + 2\, \mathbb{E}[Y^{(0)}]\mathbb{E}[Y^{(1)}] \right)\\
&amp;= \frac{1}{n} \left(\mathbb{E}\left[ \left(\frac{(1-T) Y}{1-e(x)}\right)^{2} \right] + \mathbb{E}\left[ \left(\frac{T Y}{e(x)}\right)^{2} \right] - \left(\mathbb{E}[Y^{(1)}] - \mathbb{E}[Y^{(0)}] \right)^2\right).
\end{align*}\]</span> We can further simplify this expression noting that,</p>
<p><span class="math display">\[\begin{align*}
\mathbb{E}\left[ \left( \frac{T Y}{e(X)} \right)^2 \right] &amp;=\mathbb{E}\left[\left( \frac{T Y^{(1)}}{e\left(X\right)} \right)^2\right] &amp;&amp; \text{Consistency} \\
&amp;=\mathbb{E}\left[\mathbb{1}_{\left\{T=1\right\}} \left(\frac{ Y^{(1)}}{e\left(X\right)} \right)^2\right] &amp;&amp; \text{T is binary} \\
    &amp;=\mathbb{E}\left[\mathbb{E}\left[\mathbb{1}_{\left\{T=1\right\}} \left(\frac{ Y^{(1)}}{e\left(X\right)} \right)^2 \mid X\right]\right] \\
    &amp;=\mathbb{E}\left[\frac{1}{e(X)^2}\mathbb{E}\left[\mathbb{1}_{\left\{T=1\right\}} \left( Y^{(1)} \right)^2 \mid X\right]\right] \\
    &amp;=\mathbb{E}\left[\frac{\left( Y^{(1)} \right)^2}{e(X)^2}\mathbb{E}\left[\mathbb{1}_{\left\{T=1\right\}}  \mid X\right]\right] &amp;&amp;\text{Uncounfoundness} \\
    &amp;=\mathbb{E}\left[\frac{\left( Y^{(1)} \right)^2}{e(X)^2}e(X)\right] &amp;&amp;\text{Definition of e(X)} \\
    &amp;=\mathbb{E}\left[\frac{\left( Y^{(1)} \right)^2}{e(X)}\right].
\end{align*}\]</span></p>
<p>Similarly, <span class="math display">\[\mathbb{E}\left[ \left( \frac{(1-A)Y}{1-e(X)} \right)^2 \right] = \mathbb{E}\left[\frac{\left( Y^{(0)} \right)^2}{1-e(X)}\right]. \]</span></p>
<p>Therefore, we recover the asymptotic variance for the oracle IPW <span class="math inline">\(\hat{\tau}_{\text {IPW}}^{*}\)</span>,</p>
<p><span class="math display">\[ V_{\text {\tiny IPW }}^* = \frac{1}{n} \left( \mathbb{E}\left[\frac{\left( Y^{(0)} \right)^2}{1-e(X)} + \frac{\left( Y^{(1)} \right)^2}{e(X)}\right]  - \tau^2 \right) \]</span></p>
<p>Since the variance will converge to 0 when we increase the sample size <span class="math inline">\(n\)</span> and that we also have an unbiased estimator we can conclude on consistency of <span class="math inline">\(\hat \tau_{\text{IPW}}^*\)</span>.</p>
<p><strong>Another proof of consistency:</strong> The consistency of the oracle IPW estimator can directly be shown with the weak law of large number. Denoting <span class="math inline">\(Z_i = \frac{T_{i}Y_{i}}{e(X_{i})} - \frac{(1-T_{i})Y_{i}}{1-e(X_{i})}\)</span>, and considering the series <span class="math inline">\(Z_1, Z_2, \dots, Z_n\)</span> with finite mean (<span class="math inline">\(\mathbb{E}[Z] = \tau\)</span>), then the weak law of large number gives <span class="math display">\[\begin{equation*}
\bar{Z} \stackrel{p}{\longrightarrow} \tau \quad \text { as } n \rightarrow \infty.
\end{equation*}\]</span></p>
<p>This ensures the consistency of the oracle IPW estimator.</p>
<p><strong>Asymptotic normality:</strong> We denote <span class="math inline">\(Z_i = \frac{T_{i}Y_{i}}{e(X_{i})} - \frac{(1-T_{i})Y_{i}}{1-e(X_{i})}\)</span>, we consider an iid sequence <span class="math inline">\(\left\{Z_{1}, Z_{2}, \ldots, Z_{n}\right\}\)</span> with mean <span class="math inline">\(\tau\)</span> and variance <span class="math inline">\(V_{\text{\tiny IPW}}^*:= \mathbb{E}\left[\frac{\left( Y^{(0)} \right)^2}{1-e(X)} + \frac{\left( Y^{(1)} \right)^2}{e(X)}\right] - \tau^2\)</span>. Then, the central limit theorem ensures that the sample average <span class="math inline">\(Z_{n}\)</span>, corresponding to the oracle IPW estimator, has an asymptotic standard normal distribution with mean <span class="math inline">\(\tau\)</span> and variance <span class="math inline">\(\frac{V_{\text{\tiny IPW}}^*}{n}\)</span>. We denote this,</p>
<p><span class="math display">\[\begin{equation*}
\sqrt{n}\left(\hat{\tau}_{\text{\tiny IPW}}^* - \tau \right) \stackrel{d}{\rightarrow} \mathcal{N}\left( 0,V_{\text{\tiny IPW}}^* \right)
\end{equation*}\]</span> Note that another proof is possible using M-estimation theory.</p>
</div></details>
</div>
<div class="Definition" id="inverse-propensity-weighting-estimator" title="Inverse Propensity Weighting estimator">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 6.2: </strong>Inverse Propensity Weighting estimator</summary><div>We denote by <span class="math inline">\(\hat{\tau}_{\text{\tiny IPW }}\)</span> denotes the IPW estimator, <span class="math display">\[\begin{equation*}
    \hat{\tau}_{\text {\tiny IPW }}=\frac{1}{n} \sum_{i=1}^{n}\left(\frac{T_{i} Y_{i}}{\hat{e}\left(X_{i}\right)}-\frac{\left(1-T_{i}\right) Y_{i}}{1-\hat{e}\left(X_{i}\right)}\right)   .
\end{equation*}\]</span> where <span class="math inline">\(\hat{e}\)</span> is our prediction of the propensity score.<p></p>
</div></details>
</div>
<p>Furthermore, we can show that if our estimation of the propensity score satisfies a certain condition, the under other assumption we have a convergence property of the Inverse Propensity Weighting estimator to its oracle estimator.</p>
<div class="Proposition" id="convergence-of-the-ipw-estimator-toward-its-oracle-estimator" title="convergence of the IPW estimator toward its oracle estimator">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 6.3: </strong>convergence of the IPW estimator toward its oracle estimator</summary><div>Assume that Overlap is satisfied and that there exists <span class="math inline">\(M\in\mathcal{R}^{+*}\)</span> such that <span class="math inline">\(\left|Y\right| \leq M\)</span>, and <span class="math inline">\(\sup _{x \in \mathcal{X}}|e(x)-\hat{e}(x)|=\)</span> <span class="math inline">\(\mathcal{O}_{P}\left(a_{n}\right)\)</span> where <span class="math inline">\(\left(a_{n}\right) \rightarrow 0\)</span>. Then: <span class="math display">\[|\hat{\tau}_{\text{IPW}} - \hat{\tau}_{\text{IPW}^*}| = \mathcal{O}_p\left(\frac{a_nM}{\eta^2}\right)\]</span><p></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-6.3">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div>For <span class="math inline">\(n \in \mathbb{N}^*\)</span> we have: <span class="math display">\[\begin{align*}
    |\hat{\tau}_{\text{IPW},n} - \hat{\tau}_{\text{IPW}^*,n}|&amp;= \left|\frac{1}{n}\sum_{i=1}^{n}T_{i} Y_{i}\left(\frac{1}{\hat{e}(X_{i})} -\frac{1}{e(X_{i})}\right) - (1 - T_{i})Y_{i}\left(\frac{1}{1-\hat{e}(X_{i})} -\frac{1}{1-e(X_{i})}\right)\right|\\
    &amp;\leq \left|\frac{1}{n}\sum_{i=1}^{n}T_{i} Y_{i}\left(\frac{e(X_{i})-\hat{e}(X_{i})}{\hat{e}(X_{i})e(X_{i})}\right) - (1 - T_{i})Y_{i}\left(\frac{\hat{e}(X_{i})-e(X_{i})}{(1-\hat{e}(X_{i}))(1-e(X_{i}))}\right)\right|\\
    &amp;\leq \max_{1 \leq i \leq n}  \left|T_{i} Y_{i}\left(\frac{e(X_{i})-\hat{e}(X_{i})}{\hat{e}(X_{i})e(X_{i})}\right) - (1 - T_{i})Y_{i}\left(\frac{\hat{e}(X_{i})-e(X_{i})}{(1-\hat{e}(X_{i}))(1-e(X_{i}))}\right)\right|\\
    &amp;\frac{1}{\eta}\leq \max_{1 \leq i \leq n}  \left|T_{i} Y_{i}\left(\frac{e(X_{i})-\hat{e}(X_{i})}{\hat{e}(X_{i})}\right) - (1 - T_{i})Y_{i}\left(\frac{\hat{e}(X_{i})-e(X_{i})}{1-\hat{e}(X_{i})}\right)\right| &amp;&amp; \text{Overlap} \\
    &amp;\leq \frac{2}{\eta^2}\max_{1 \leq i \leq n}  \left|T_{i} Y_{i}\left(e(X_{i})-\hat{e}(X_{i})\right) - (1 - T_{i})Y_{i}\left(\hat{e}(X_{i})-e(X_{i})\right)\right| &amp;&amp; \text{(*)} \\
    &amp;\leq \frac{2M}{\eta^2} \max_{1 \leq i \leq n} |e(X_{i})-\hat{e}(X_{i})| &amp;&amp; \left|Y\right| \leq M\\
\end{align*}\]</span><p></p>
<p>where in <span class="math inline">\((*)\)</span> we used the fact that there exista a big enough <span class="math inline">\(n\)</span> such that <span class="math inline">\(\frac{\eta}{2} \leq \hat{e}(X_{i}) \leq 1- \frac{\eta}{2}\)</span> since we have that <span class="math inline">\(\sup _{x \in \mathcal{X}}|e(x)-\hat{e}(x)|=\)</span> <span class="math inline">\(\mathcal{O}_{P}\left(a_{n}\right)\)</span>, and that <span class="math inline">\(|\hat{\tau}_{\text{IPW},n} - \hat{\tau}_{\text{IPW}^*,n}| \leq \frac{2M}{\eta^2} \max_{1 \leq i \leq n} |e(X_{i})-\hat{e}(X_{i})|\)</span></p>
<p>Therefore, we have that: <span class="math display">\[|\hat{\tau}_{\text{IPW}} - \hat{\tau}_{\text{IPW}^*}| = \mathcal{O}_p\left(\frac{a_nM}{\eta^2}\right)\]</span></p>
</div></details>
</div>
<p>Hence, using now both previuos propotions we can built the main theorem of the IPW estimator.</p>
<div class="Theorem" id="asymptotic-properties-of-hattau_texttiny-ipw" title="Asymptotic properties of \hat{\tau}_{\text{\tiny IPW }}">
<p></p><details class="Theorem fbx-simplebox fbx-default" open=""><summary><strong>Theorem 6.1: </strong>Asymptotic properties of <span class="math inline">\(\hat{\tau}_{\text{\tiny IPW }}\)</span></summary><div>Assume that Overlap is satisfied and that there exists <span class="math inline">\(M\in\mathcal{R}^{+*}\)</span> such that <span class="math inline">\(\left|Y\right| \leq M\)</span>, and <span class="math inline">\(\sup _{x \in \mathcal{X}}|e(x)-\hat{e}(x)|=\)</span> <span class="math inline">\(\mathcal{O}_{P}\left(a_{n}\right)\)</span> where <span class="math inline">\(\left(a_{n}\right) \rightarrow 0\)</span>, then: The IPW estimator, denoted $ _{}$, is consistent, <span class="math display">\[\hat{\tau}_{\text{\tiny IPW}} \stackrel{p}{\longrightarrow} \tau, \]</span><p></p>
<p>and is an asymptotically normal estimator, that is,</p>
<p><span class="math display">\[\sqrt{n}\left(\hat{\tau}_{\text{\tiny IPW}} - \tau \right) \stackrel{d}{\rightarrow} \mathcal{N}\left(0, V_{\text {\tiny IPW }^*}\right),\]</span></p>
<p>where, <span class="math display">\[V_{\text {\tiny IPW }}^{*} = \mathbb{E}\left[\frac{\left( Y^{(0)} \right)^2}{1-e(X)} + \frac{\left( Y^{(1)} \right)^2}{e(X)}\right]  - \tau^2.\]</span></p>
<p>Furthermore, if <span class="math inline">\(\left(a_{n}\right)\)</span> converges to <span class="math inline">\(0\)</span> at a <span class="math inline">\(\sqrt{n}\)</span>-rate we can show that <span class="math inline">\(\hat{\tau}{\text{\tiny IPW}}\)</span> is <span class="math inline">\(\sqrt{n}\)</span> consistent.</p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-6.4">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div>We compare the IPW estimator with the oracle one, and we write several inequalities being,<p></p>
<p><span class="math display">\[\begin{align*}
    |\hat{\tau}_{\text{\tiny IPW}} - \tau| &amp;= |\hat{\tau}{\text{\tiny IPW}} - \tau{\text{\tiny IPW}}^* + \tau{\text{\tiny IPW}}^* - \tau| \\
    &amp;\leq |\hat{\tau}{\text{\tiny IPW}}- \tau{\text{\tiny IPW}}^*| + |\tau{\text{\tiny IPW}}^* - \tau|
\end{align*}\]</span></p>
<p>We already showed that the oracle IPW estimator is consistent and asymptotically normally distributed. We also showed that <span class="math inline">\(|\hat{\tau}_{\text{IPW}} - \tau_{\text{IPW}^*}| = \mathcal{O}_p\left(\frac{a_nM}{\eta}\right)\)</span>. Therefore using the inequality from above we get that $ _{}$, is consistent.</p>
<p>Furthermore if we assume that <span class="math inline">\(\left(a_{n}\right)\)</span> converges to <span class="math inline">\(0\)</span> at a <span class="math inline">\(\sqrt{n}\)</span>-rate we can write:</p>
<p><span class="math display">\[\begin{equation*}
    \sqrt{n} (\hat \tau_{\text{\tiny IPW}} - \tau) = \underbrace{\sqrt{n} (\hat \tau_{\text{\tiny IPW}}  - \tau_{\text{\tiny IPW}} ^*)}_\textrm{$\stackrel{p}{\longrightarrow} 0$}  +  \underbrace{\sqrt{n}(\tau_{\text{\tiny IPW}} ^* - \tau)}_\textrm{$\stackrel{\mathcal{L} }{\rightarrow} \mathcal{N}\left(0, V_{\text{\tiny IPW}}^* \right)$},
\end{equation*}\]</span> And we can conclude that <span class="math inline">\(\hat{\tau}{\text{\tiny IPW}}\)</span> is <span class="math inline">\(\sqrt{n}\)</span> consistent and its variance is the same as <span class="math inline">\(\tau_{\text{\tiny IPW}}^*\)</span>.</p>
</div></details>
</div>
<p>Therefore, if we can estimate the propensity score for all individuals then we can use IPW estimator estimator to compute the ATE. However, the IPW estimator has many problems. In particular, it is not invariant to translation of the outcome. For example, if we change <span class="math inline">\(Y\)</span> to <span class="math inline">\(Y + c\)</span> with <span class="math inline">\(c\)</span> a constant , then we get: <span class="math display">\[\begin{align*}
    \hat{\tau}_{\text{\tiny IPW}}^{bis} &amp;= \frac{1}{n} \sum_{i=1}^{n}\left(\frac{T_{i} (Y_{i} + c)}{\hat{e}\left(X_{i}\right)}-\frac{\left(1-T_{i}\right) (Y_{i}+c)}{1-\hat{e}\left(X_{i}\right)}\right)\\
    &amp;= \hat{\tau}_{\text{\tiny IPW}} + c\left( \sum_{i=1}^n \frac{T_i}{\hat{e}\left(X_{i}\right)} - \frac{1-T_i}{1-\hat{e}\left(X_{i}\right)}\right)
\end{align*}\]</span> If we have the true propensity score, then <span class="math inline">\(\sum_{i=1}^n \frac{T_i}{\hat{e}\left(X_{i}\right)} - \frac{1-T_i}{1-\hat{e}\left(X_{i}\right)}\)</span> should converge to 0. However, in general, it is not equal to 0 in finite samples. Since adding a constant to every outcome should not change the average causal effect, this estimator is not reasonable because of its dependence on <span class="math inline">\(c\)</span>.</p>
<p>A simple fix to the problem is to normalize the weights of our IPW estimator:</p>
<div class="Definition" id="oracle-inverse-propensity-weighting-estimator-with-normalization" title="Oracle Inverse Propensity Weighting estimator with normalization">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 6.3: </strong>Oracle Inverse Propensity Weighting estimator with normalization</summary><div>Assume the propensity score <span class="math inline">\(e(X)\)</span> is a known function, then $ _{}^{*}$ denotes the oracle normalized IPW estimator, <span class="math display">\[\begin{equation*}
\hat{\tau}_{\text {\tiny IPW norm.}}^*=\left(\sum_{i=1}^{n} \frac{T_{i}}{e\left(X_{i}\right)}\right)^{-1} \sum_{i=1}^{n} \frac{T_{i} Y_{i}}{e\left(X_{i}\right)}-\left(\sum_{i=1}^{n} \frac{1-T_{i}}{1- e\left(X_{i}\right)}\right)^{-1} \sum_{i=1}^{n} \frac{\left(1-T_{i}\right) Y_{i}}{1-e\left(X_{i}\right)} .
\end{equation*}\]</span><p></p>
</div></details>
</div>
<div class="Proposition" id="oracle-normalized-ipw-unbiasedness" title="Oracle normalized IPW unbiasedness">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 6.4: </strong>Oracle normalized IPW unbiasedness</summary><div>The oracle normalized IPW, denoted <span class="math inline">\(\hat{\tau}_{\text {\tiny IPW, norm }}^{*}\)</span>, is an unbiased estimator of the average treatment effect <span class="math inline">\(\tau\)</span>, that is,<p></p>
<p><span class="math display">\[\begin{equation*}
    \mathbb{E}[\hat{\tau}_{\text {\tiny IPW, norm }}^{*}] = \tau.
\end{equation*}\]</span></p>
</div></details>
</div>

</div>
