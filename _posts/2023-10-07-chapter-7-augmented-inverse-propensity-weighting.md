---
layout: post
title: "Chapter 7 — Augmented Inverse Propensity Weighting"
date: 2023-10-07
excerpt: "The doubly-robust AIPW estimator: combining outcome modelling and propensity weighting with semiparametric efficiency."
---

<div class="course-chapter">
<p class="chapter-nav">
  Course: <a href="/blog/">Finite Sample and Asymptotic Estimators in Causal Inference</a>
</p>

<p>An alternative estimator is the augmented inverse probability weighted estimator (AIPW). It combines both the properties of the regression based estimator and the inverse probability weighted estimator. It is therefore a ‘doubly robust’ method in that it only requires either the propensity or outcome model to be correctly specified but not both. This model holds the same assumptions as the Inverse Probability Weighted Estimator (IPW).</p>
<p>Here’s a brief overview of how the AIPW estimator works:</p>
<ul>
<li><strong>Inverse Probability Weighting:</strong> The first step in AIPW involves estimating the probabilities of receiving the treatment (propensity scores) and not receiving the treatment for each individual in the study based on their observed covariates (confounding variables). This is typically done using logistic regression or other modeling techniques. Each individual’s outcome is weighted by the inverse of their propensity score. This weighting gives more importance to the outcomes of individuals whose treatment assignment is less predictable based on their covariates.</li>
<li><strong>Outcome Mode:l</strong> You then fit a model to predict the outcome variable based on treatment status and covariates. This model estimates the expected outcome for each individual under both treatment and control conditions.</li>
<li><strong>AIPW Estimation:</strong> The AIPW estimator combines the results from steps 1 and 2. It calculates the difference between the expected outcomes under treatment and control for each individual, weighted by the inverse propensity score. Summing these weighted differences provides an estimate of the average treatment effect while accounting for potential bias due to confounding. \end{enumerate}</li>
</ul>
<p>The AIPW estimator is particularly useful when there are complex interactions and confounding variables in observational studies. By adjusting for the estimated propensity scores and using inverse probability weighting, it helps to mitigate bias and provide more accurate estimates of treatment effects.</p>
<p>It’s important to note that while the AIPW estimator can be a powerful tool for causal inference, it relies on the assumption that the estimated propensity scores are correctly specified and that there are no unmeasured confounding variables. Careful consideration of model assumptions and sensitivity analyses are typically conducted when using the AIPW estimator in practice.</p>
<div class="Definition" id="oracle-augmented-inverse-propensity-weighting-estimator" title="Oracle Augmented Inverse Propensity Weighting estimator">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 7.1: </strong>Oracle Augmented Inverse Propensity Weighting estimator</summary><div>We denote <span class="math inline">\(\hat \tau_{\text{AIPW}}^*\)</span> the oracle AIPW estimator, where all the nuisance parameters are supposed to be known, such that: <span class="math display">\[\begin{align*}
    \hat \tau_{\text{AIPW}}^* &amp;= \frac{1}{|\mathcal{I}|}\sum_{i \in \mathcal{I}}\left(\mu_{(1)}(X_i) - \mu_{(0)}(X_i) + \frac{T_i.(Y_i - \mu_{(1)}(X_i))}{e(X_i)}- \frac{(1 - T_i)(Y_i-\mu_{(0)}(X_i))}{1 - e(X_i)}\right)
\end{align*}\]</span> where <span class="math inline">\(\mu_{(t)}(X) = \mathbb{E}\left[Y | T=t,X\right]\)</span><p></p>
</div></details>
</div>
<div class="Proposition" id="asymptotic-properties-of-hat-tau_textaipw" title="Asymptotic properties of \hat \tau_{\text{AIPW}}^*">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 7.1: </strong>Asymptotic properties of <span class="math inline">\(\hat \tau_{\text{AIPW}}^*\)</span></summary><div>The oracle AIPW, denoted <span class="math inline">\(\hat \tau_{\text{AIPW}}^*\)</span>, is consistent, <span class="math display">\[\hat \tau_{\text{AIPW}}^* \stackrel{p}{\longrightarrow} \tau, \]</span><p></p>
<p>and is an asymptotically normal estimator, that is,</p>
<p><span class="math display">\[\sqrt{n}\left(\hat \tau_{\text{AIPW}}^* - \tau \right) \stackrel{d}{\rightarrow} \mathcal{N}\left(0, V_{\text {\tiny AIPW }}^*\right),\]</span></p>
<p>where, <span class="math display">\[V_{\text{AIPW}}^* =\mathbb{E}\left[ \frac{\left(Y^{(1)}-\mu_1(X)\right)^2 }{e(X)} \right]+\mathbb{E}\left[ \frac{(Y^{(0)}-\mu_0(X))^2}{1-e(X)}  \right] +   \operatorname{Var}[\mu_1(X) - \mu_0(X)].\]</span></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-7.1">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div>This oracle doubly-robust estimator can be understood as an M-estimation problem where a function <span class="math inline">\(\Psi(.)\)</span> can be introduced such that<p></p>
<p><span class="math display">\[\psi(X, A, Y, \boldsymbol{\theta})=\left(\begin{array}{l}
A\frac{Y-\mu_1(X)}{e(X)} + \mu_1(X)-\theta_{0} \\
(1-A)\frac{Y-\mu_0(X)}{1-e(X)} + \mu_0(X)-\theta_{1} \\
\left(\theta_{0}-\theta_{1}\right)-\theta_{2}
\end{array}\right).\]</span></p>
<p>Ensuring the condition <span class="math inline">\(\mathbb{E}[\psi(X, T, Y, \boldsymbol{\theta})] = \boldsymbol{0}\)</span>, where <span class="math inline">\(\boldsymbol{\theta} = (\theta_0, \theta_1, \theta_2))\)</span> gives, <span class="math display">\[\begin{align*}
\theta_0 &amp;= \mathbb{E}\left[ T\frac{Y-\mu_1(X)}{e(X)} + \mu_1(X)\right]     \\
&amp;= \mathbb{E}\left[ T\frac{Y}{e(X)}\right] - \mathbb{E}\left[ A\frac{\mu_1(X)}{e(X)}\right]  + \mathbb{E}\left[\mu_1(X)\right]   \\
&amp;= \mathbb{E}\left[ \mathbb{E}[T\frac{Y}{e(X)} \mid X ]\right] - \mathbb{E}\left[ T\frac{\mathbb{E}[Y^{(1)} \mid X, T = 1]}{e(X)}\right]  + \mathbb{E}\left[\mu_1(X)\right]  \\
&amp;= \mathbb{E}\left[ T\frac{\mathbb{E}[Y^{(1)} \mid X, T = 1]}{e(X)}\right]  - \mathbb{E}\left[ T\frac{\mathbb{E}[Y^{(1)} \mid X, T = 1]}{e(X)}\right]  + \mathbb{E}\left[\mu_1(X)\right]  \\
&amp;= \mathbb{E}\left[\mu_1(X)\right] \\
&amp;= \mathbb{E}\left[Y^{(1)}\right],
\end{align*}\]</span></p>
<p>and similarly <span class="math display">\[\theta_1  = \mathbb{E}\left[\mu_0(X)\right] = \mathbb{E}\left[Y^{(0)}\right],\]</span> so that <span class="math display">\[\theta_2 = \tau.\]</span></p>
<p>Derivations around this function <span class="math inline">\(\psi(.)\)</span> gives,</p>
<p><span class="math display">\[\frac{\partial \psi}{\partial \theta} (X, A, Y, \theta)=\left(\begin{array}{ccc}
-1 &amp; 0 &amp; 0 \\
0 &amp; -1 &amp; 0 \\
1 &amp; -1 &amp; -1
\end{array}\right) \quad \Rightarrow \quad A\left(\boldsymbol{\theta} \right)= \left(\begin{array}{ccc}
1 &amp; 0 &amp; 0 \\
0 &amp; 1 &amp; 0 \\
-1 &amp; 1 &amp; 1
\end{array}\right).\]</span></p>
<p>In particular,</p>
<p><span class="math display">\[A^{-1}\left(\boldsymbol{\theta} \right)= \left(\begin{array}{ccc}
1 &amp; 0 &amp; 0 \\
0 &amp; 1 &amp; 0 \\
1 &amp; -1 &amp; 1
\end{array}\right)\]</span></p>
<p><span class="math display">\[\left(A^{-1}\left(\boldsymbol{\theta} \right)\right)^{T}= \left(\begin{array}{ccc}
1 &amp; 0 &amp; 1 \\
0 &amp; 1 &amp; -1 \\
0 &amp; 0 &amp; 1
\end{array}\right)\]</span></p>
<p>On the other hand, denoting</p>
<p><span class="math display">\[m_1(X,T,Y) := T\frac{Y-\mu_1(X)}{e(X)} + \mu_1(X),\]</span> and <span class="math display">\[m_0(X,T,Y) := (1-T)\frac{Y-\mu_0(X)}{1-e(X)} + \mu_0(X),\]</span></p>
<p>one can obtain <span class="math display">\[\mathbb{E}[\psi  \cdot \psi^T] =\left(\begin{array}{ccc}
\mathbb{E}[\left(m_1(X,T,Y)-\theta_{0}\right)^{2}] &amp; \mathbb{E}[\left(m_1(X,T,Y)-\theta_{0}\right)\left(m_0(X,T,Y)-\theta_{1}\right)] &amp; 0 \\
\mathbb{E}[\left(m_1(X,T,Y)-\theta_{0}\right)\left(m_0(X,T,Y)-\theta_{1}\right)] &amp; \mathbb{E}[\left(m_0(X,T,Y)-\theta_{1}\right)^{2}] &amp; 0 \\
0 &amp; 0 &amp; 0
\end{array}\right).\]</span></p>
<p>Computing <span class="math inline">\(V = A^{-1}\, \mathbb{E}[\psi \cdot \psi^T]\, \left(A^{-1}\right)^{T}\)</span> gives the following asymptotic variance</p>
<p><span class="math display">\[\begin{equation*}
     V_{3,3} = \mathbb{E}[\left(m_1(X,T,Y)-\theta_{0}\right)^{2}] + \mathbb{E}[\left(m_0(X,T,Y)-\theta_{1}\right)^{2}]. \\
\end{equation*}\]</span></p>
<p>This expression can be further developed noting that,</p>
<p><span class="math display">\[\begin{equation*}
    \mathbb{E}[\left(m_1(X,T,Y)-\theta_{0}\right)^{2}] = \mathbb{E}\left[ \left(T\frac{Y-\mu_1(X)}{e(X)} \right)^2 \right]+ 2\,\mathbb{E}[(T\frac{Y-\mu_1(X)}{e(X)})\,(\mu_1(X) - \theta_0)] + \mathbb{E}[(\mu_1(X)- \theta_0)^2]
\end{equation*}\]</span> Using Consistency, Unconfoundedness, and definition or <span class="math inline">\(\mu_1(X) = \mathbb{E}[Y \mid X, T=1]\)</span>, <span class="math display">\[\begin{align*}
    \mathbb{E}\left[ \left(T\frac{Y-\mu_1(X)}{e(X)} \right)^2 \right] &amp;=   \mathbb{E}\left[ \left(T\frac{Y^{(1)}-\mu_1(X)}{e(X)} \right)^2 \right] &amp;&amp; \text{Consistency} \\
    &amp;=\mathbb{E}\left[ \mathbb{E}\left[\left(T\frac{Y^{(1)}-\mu_1(X)}{e(X)} \right)^2 \mid X \right]\right] &amp;&amp; \text{Total expectation}\\
    &amp;= \mathbb{E}\left[ \mathbb{E}\left[T\left(\frac{Y^{(1)}-\mu_1(X)}{e(X)} \right)^2 \mid X \right]\right] &amp;&amp; \text{T is binary}\\
    &amp;= \mathbb{E}\left[ \mathbb{E}\left[\mathbb{1}_{\left\{T=1\right\}}\left(\frac{Y^{(1)}-\mu_1(X)}{e(X)} \right)^2 \mid X \right]\right] &amp;&amp; \text{T written as an indicator} \\
     &amp;= \mathbb{E}\left[ \frac{1}{e(X)^2} \mathbb{E}\left[\mathbb{1}_{\left\{T=1\right\}}\left(Y^{(1)}-\mu_1(X)\right)^2 \mid X \right]\right] &amp;&amp; \text{$e(X)$ is a function of $X$} \\
      &amp;= \mathbb{E}\left[ \frac{\left(Y^{(1)}-\mu_1(X)\right)^2 }{e(X)^2} \mathbb{E}\left[\mathbb{1}_{\left\{T=1\right\}}\mid X \right]\right] &amp;&amp; \text{Uncounf. \&amp; $\mu_1(.)$ is func. of $X$} \\
      &amp;= \mathbb{E}\left[ \frac{\left(Y^{(1)}-\mu_1(X)\right)^2 }{e(X)^2} e(X)\right] &amp;&amp; \text{Definition of $e(X)$} \\
      &amp;= \mathbb{E}\left[ \frac{\left(Y^{(1)}-\mu_1(X)\right)^2 }{e(X)} \right], \\
\end{align*}\]</span></p>
<p>And we also have that:</p>
<p><span class="math display">\[\begin{align*}
    2\,\mathbb{E}[(T\frac{Y-\mu_1(X)}{e(X)})\,(\mu_1(X) - \theta_0)] &amp;=  2\,\mathbb{E}[ T\frac{Y\mu_1(X)}{e(X)} - T\frac{\mu_1(X)^2}{e(X)} -\theta_1 T\frac{Y}{e(X)} + \theta_0 \frac{\mu_1(X)}{e(X)}]\\
    &amp;= 2\,\mathbb{E}[ T\mu_1(X)\frac{Y - \mu_1(X)}{e(X)}] - 2\theta_1\,\mathbb{E}[ T\frac{Y}{e(X)}] + 2\theta_0\,\mathbb{E}[ \frac{\mu_1(X)}{e(X)}] \\
    &amp;= 2\,\mathbb{E}[ \frac{T\mu_1(X)Y}{e(X)}] - 2\,\mathbb{E}[T \frac{\mu_1(X)^2}{e(X)}] -2\theta_1\theta_0 + 2\theta_0 \mathbb{E}[ \frac{\mu_1(X)}{e(X)}]\\
    &amp;= 2\,\mathbb{E}\left[\mathbb{E}[ \frac{T\mu_1(X)Y}{e(X)}\mid X]\right] - 2\,\mathbb{E}[T \frac{\mu_1(X)^2}{e(X)}] -2\theta_1\theta_0 + 2\theta_0 \mathbb{E}[ \frac{\mu_1(X)}{e(X)}] \\
    &amp;= 2\,\mathbb{E}[T \frac{\mu_1(X)^2}{e(X)}] - 2\,\mathbb{E}[T \frac{\mu_1(X)^2}{e(X)}] -2\theta_1\theta_0 + 2\theta_0 \mathbb{E}[ \frac{\mu_1(X)}{e(X)}] \\
    &amp;= 0 - 2\theta_1\theta_0 + 2\theta_0 \mathbb{E}[ \frac{\mu_1(X)}{e(X)}] \\
    &amp;= - 2\theta_1\theta_0 + 2\theta_0 \mathbb{E}[ \frac{\mathbb{E}[Y \mid X, T=1]}{e(X)}] \\
    &amp;= - 2\theta_1\theta_0 + 2\theta_0 \mathbb{E}[ \mathbb{E}[\frac{TY}{e(X)} \mid X, T=1]]  \\
    &amp;= - 2\theta_1\theta_0 + 2\theta_1\theta_0  \\
    &amp;=0
\end{align*}\]</span></p>
<p>Finally, <span class="math display">\[\begin{equation*}
    \mathbb{E}[\left(m_1(X,T,Y)-\theta_{0}\right)^{2}] = \mathbb{E}\left[ \frac{\left(Y^{(1)}-\mu_1(X)\right)^2}{e(X)} \right] + \mathbb{E}[(\mu_1(X)- \theta_0)^2].
\end{equation*}\]</span></p>
<p>On the other side, and similarly, one can show that <span class="math display">\[\begin{equation*}
    \mathbb{E}[\left(m_0(X,T,Y)-\theta_{1}\right)^{2}] = \mathbb{E}\left[\frac{(Y^{(0)}-\mu_0(X))^2}{1-e(X)}  \right] + \mathbb{E}[(\mu_0(X)- \theta_1)^2].
\end{equation*}\]</span></p>
<p>Therefore,</p>
<p><span class="math display">\[\hat \tau_{\text{AIPW}}^* \stackrel{p}{\longrightarrow} \tau\]</span></p>
<p>where <span class="math display">\[\begin{equation*}
    V_{\text{AIPW}}^* =\mathbb{E}\left[ \frac{\left(Y^{(1)}-\mu_1(X)\right)^2 }{e(X)} \right]+\mathbb{E}\left[ \frac{(Y^{(0)}-\mu_0(X))^2}{1-e(X)}  \right] +  \mathbb{E}[(\mu_0(X)- \theta_1)^2] + \mathbb{E}[(\mu_1(X)- \theta_0)^2].  \\
\end{equation*}\]</span></p>
<p>The large sample variance can be expressed a bit differently using the following derivations,</p>
<p><span class="math display">\[\begin{equation*}
    \operatorname{Var}[\mu_1(X) - \mu_0(X)] = \mathbb{E}[(\mu_0(X)- \theta_1)^2] + \mathbb{E}[(\mu_1(X)- \theta_0)^2] + 2(\theta_1\theta_0 - \mathbb{E}[\mu_1(X)\mu_0(X)]).
\end{equation*}\]</span></p>
<p>As <span class="math inline">\(\mu_1(X) \perp\mkern-9.5mu\perp \mu_0(X) \mid X\)</span>, <span class="math display">\[\begin{equation*}
    \operatorname{Var}[\mu_1(X) - \mu_0(X)] = \mathbb{E}[(\mu_0(X)- \theta_1)^2] + \mathbb{E}[(\mu_1(X)- \theta_0)^2].
\end{equation*}\]</span></p>
<p>Finally,</p>
<p><span class="math display">\[\begin{equation*}
    V_{\text{AIPW}}^* =\mathbb{E}\left[ \frac{\left(Y^{(1)}-\mu_1(X)\right)^2 }{e(X)} \right]+\mathbb{E}\left[ \frac{(Y^{(0)}-\mu_0(X))^2}{1-e(X)}  \right] +   \operatorname{Var}[\mu_1(X) - \mu_0(X)].  \\
\end{equation*}\]</span> <strong>Another proof of consistency:</strong> The consistency of the oracle IPW estimator can directly be shown with the weak law of large number. Denoting <span class="math display">\[\begin{equation*}
Z_i = \mu_{(1)}(X_i) - \mu_{(0)}(X_i) + \frac{T_i.(Y_i - \mu_{(1)}(X_i))}{e(X_i)}- \frac{(1 - T_i)(Y_i-\mu_{(0)}(X_i))}{1 - e(X_i)}
\end{equation*}\]</span> And we consider the iid series <span class="math inline">\(Z_1, Z_2, \dots, Z_n\)</span> with finite mean (<span class="math inline">\(\mathbb{E}[Z] = \tau\)</span>), then the weak law of large number gives <span class="math display">\[\begin{equation*}
\bar{Z} \stackrel{p}{\longrightarrow} \tau \quad \text { as } n \rightarrow \infty.
\end{equation*}\]</span></p>
<p>This ensures the consistency of the oracle AIPW estimator.</p>
<p><strong>Asymptotic normality:</strong> We consider the iid sequence <span class="math inline">\(\left\{Z_{1}, Z_{2}, \ldots, Z_{n}\right\}\)</span> with mean <span class="math inline">\(\tau\)</span> and variance <span class="math inline">\(V_{\text{\tiny AIPW}}^*\)</span>. Then, the central limit theorem ensures that the sample average <span class="math inline">\(Z_{n}\)</span>, corresponding to the oracle IPW estimator, has an asymptotic standard normal distribution with mean <span class="math inline">\(\tau\)</span> and variance <span class="math inline">\(\frac{V_{\text{\tiny AIPW}}^*}{n}\)</span>. We denote this,</p>
<p><span class="math display">\[\begin{equation*}
\sqrt{n}\left(\hat{\tau}_{\text{\tiny IPW}}^* - \tau \right) \stackrel{d}{\rightarrow} \mathcal{N}\left( 0,V_{\text{\tiny AIPW}}^* \right)
\end{equation*}\]</span></p>
</div></details>
</div>
<p>Now, the oracle AIPW will be compared to the AIPW estimator where the nuisance function are fitted on an hold out set of data. First we need to make a new assumption about the product of the residuals of propensity score and the response function.</p>
<div class="Definition" id="crossfitted-augmented-inverse-propensity-weighting-estimator" title="Crossfitted Augmented Inverse Propensity Weighting estimator">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 7.2: </strong>Crossfitted Augmented Inverse Propensity Weighting estimator</summary><div>We denote <span class="math inline">\(\tilde\tau_{\text{AIPW}}^*\)</span> the crossfitted AIPW estimator, where <span class="math inline">\(\mathcal{I}_1, \mathcal{I}_2,..., \mathcal{I}_K\)</span> are splited data such that: <span class="math display">\[\forall i, j \text{  \quad } \mathcal{I}_i \cap \mathcal{I}_j = \varnothing \text{ and } \bigcup_{k=1}^K \mathcal{I}_k = \mathcal{I}\]</span><p></p>
<p><span class="math display">\[\begin{align*}
    \tilde \tau_{\text{AIPW}}^* &amp;=\frac{1}{|\mathcal{I}|} \sum_{k = 1}^K \sum_{i \in \mathcal{I_k}}\left(\hat\mu_{(1)}^{\bar{\mathcal{I}_k}}(X_i) - \hat\mu_{(0)}^{\bar{\mathcal{I}_k}}(X_i) + \frac{T_i.(Y_i - \hat\mu_{(1)}^{\bar{\mathcal{I}_k}}(X_i))}{\hat e^{\bar{\mathcal{I}_k}}(X_i)}- \frac{(1 - T_i)(Y_i-\hat\mu_{(0)}^{\bar{\mathcal{I}_k}}(X_i))}{1 - \hat e^{\bar{\mathcal{I}_k}}(X_i)}\right)
\end{align*}\]</span> where <span class="math inline">\(\hat\mu_{(t)}^{\bar{\mathcal{I}_k}}(X)\)</span> and <span class="math inline">\(\hat e^{\bar{\mathcal{I}_k}}(X)\)</span> are the estimates of <span class="math inline">\(\mu_{(t)}\)</span> and <span class="math inline">\(e\)</span> obtained using only the sample <span class="math inline">\(\bar{\mathcal{I}_k}\)</span>.</p>
</div></details>
</div>
<div class="Proposition" id="convergence-of-the-crossfitted-aipw-estimator-toward-its-oracle-estimator" title="Convergence of the crossfitted AIPW estimator toward its oracle estimator">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 7.2: </strong>Convergence of the crossfitted AIPW estimator toward its oracle estimator</summary><div>Assume that Overlap is satisfied and that for <span class="math inline">\(t\in\{0,1\}\)</span>: <span class="math display">\[\sup _{x \in \mathcal{X}}|(\mu_t^{\mathcal{I}}(X)-\hat{\mu_t}(x))^{\frac{1}{2}}(e(x)-\hat{e}^{\mathcal{I}}(x))^{\frac{1}{2}}|=\mathcal{O}_{P}\left(\frac{1}{\sqrt{n}}\right)\]</span> then: <span class="math display">\[\sqrt{n}(\tilde{\tau}_{\text{\tiny AIPW}}-\hat{\tau}_{\text{\tiny AIPW}}^{*}) \stackrel{p}{\longrightarrow} 0, \]</span><p></p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-7.2">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div>First we introduce,<p></p>
<p><span class="math display">\[m_1(X,T,Y) := T\frac{Y- \mu_1(X)}{ e(X)} +  \mu_1(X),\]</span> <span class="math display">\[m_0(X,T,Y) := (1-T)\frac{Y- \mu_0(X)}{1- e(X)} +  \mu_0(X),\]</span></p>
<p>and,</p>
<p><span class="math display">\[\hat m_1^k(X,T,Y) := T\frac{Y-\hat \mu_1^{\bar{\mathcal{I}_k}}(X)}{\hat e^{\bar{\mathcal{I}_k}}(X)} + \hat \mu_1^{\bar{\mathcal{I}_k}}(X),\]</span> <span class="math display">\[\hat m_0^k(X,T,Y) := (1-T)\frac{Y-\hat \mu_0^{\bar{\mathcal{I}_k}}(X)}{1-\hat e^{\bar{\mathcal{I}_k}}(X)} + \hat \mu_0^{\bar{\mathcal{I}_k}}(X),\]</span> the same quantities as previously but where nuisance parameters are estimated with the hold out data set. The difference between the oracle estimator and the AIPW estimator can be decomposed such as,</p>
<p><span class="math display">\[\begin{align*}
    \sqrt{n}\, \left( \tilde \tau_{\text{AIPW}} - \hat\tau_{\text{AIPW}}^*\right) &amp;=  \sqrt{n}\, \frac{1}{|\mathcal{I}|}\sum_{k = 1}^K \sum_{i \in \mathcal{I_k}} \left( \hat m_1^k(X_i,T_i,Y_i) - m_1(X_i,T_i,Y_i)\right)  - \left( \hat m_0^k(X_i,T_i,Y_i) - m_0(X_i,T_i,Y_i)\right).
\end{align*}\]</span></p>
<p>Then, <span class="math display">\[\begin{align*}
\sqrt{n}\, \frac{1}{|\mathcal{I}|} \sum_{i \in \mathcal{I_k}} (\hat m^k_1- m_1)(X_i,T_i,Y_i)
=&amp; \frac{1}{\sqrt{n}} \sum_{i \in \mathcal{I_k}}\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)+T_{i} \frac{Y_{i}-\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)}{\hat{e}\left(X_{i}\right)}-\mu_{1}\left(X_{i}\right)-T_{i} \frac{Y_{i}-\mu_{1}\left(X_{i}\right)}{e\left(X_{i}\right)}\right) \\
=&amp; \frac{1}{\sqrt{n}}  \sum_{i \in \mathcal{I_k}}\left(\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)\right) &amp;&amp; \text{Further denoted $A_n^k$}\\
&amp;+\frac{1}{\sqrt{n}}  \sum_{i \in \mathcal{I_k}} T_{i}\left(\left(Y_{i}-\mu_{1}\left(X_{i}\right)\right)\left(\frac{1}{\hat{e}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right)\right) &amp;&amp; \text{Further denoted $B_n^k$}\\
&amp;-\frac{1}{\sqrt{n}}  \sum_{i \in \mathcal{I_k}} T_{i}\left(\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(\frac{1}{\hat{e}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right)\right).&amp;&amp; \text{Further denoted $C_n^k$}
\end{align*}\]</span></p>
<p>The first two terms can be demonstrated to converge toward 0 in probability. To do this, one can show that each of these two first terms converge in <span class="math inline">\(L^2\)</span> norm.</p>
<p>First, one can show that the expectation of <span class="math inline">\(\frac{A_n^k}{\sqrt{n}}\)</span> is null,</p>
<p><span class="math display">\[\begin{align*}
     \mathbb{E}\left[\frac{1}{n} \sum_{i \in \mathcal{I_k}}\left(\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)\right) \right]
     &amp;= \frac{1}{n} \sum_{i \in \mathcal{I_k}}\mathbb{E}\left[\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)\right] \\
     &amp;= \frac{|\mathcal{I_k}|}{n} \mathbb{E}\left[\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X\right)-\mu_{1}\left(X\right)\right)\left(1-\frac{T}{e\left(X\right)}\right)\right] &amp;&amp; \text{i.i.d.} \\
     &amp;= \frac{|\mathcal{I_k}|}{n} \mathbb{E}\left[ \mathbb{E}\left[ \left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X\right)-\mu_{1}\left(X\right)\right)\left(1-\frac{T}{e\left(X\right)}\right)\mid X\right] \right] \\
     &amp;= \frac{|\mathcal{I_k}|}{n}  \mathbb{E}\left[\mathbb{E}\left[ \left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X\right)-\mu_{1}\left(X\right)\right)\left(1-\frac{\mathbb{E}\left[T\mid X \right] }{e\left(X\right)}\right)\right]\right] \\
     &amp;= \frac{|\mathcal{I_k}|}{n}  \mathbb{E}\left[\mathbb{E}\left[ \left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X\right)-\mu_{1}\left(X\right)\right)\left(1-\frac{e\left(X\right) }{e\left(X\right)}\right)\right]\right] \\
     &amp;= 0.
\end{align*}\]</span></p>
<p>This will be helpful in the next series of derivations.</p>
<p>Now, consider the expectation of the square of <span class="math inline">\(\frac{A_n^k}{\sqrt{n}}\)</span>,</p>
<p><span class="math display">\[\begin{align*}
    \mathbb{E}\left[ \left(\frac{1}{n}  \sum_{i \in \mathcal{I_k}}\left(\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)\right)\right)^2 \right]
    &amp;= \operatorname{Var}\left[ \frac{1}{n}  \sum_{i \in \mathcal{I_k}}\left(\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)\right) \right] \\
    &amp;= \frac{1}{n^2} \operatorname{Var}\left[  \sum_{i \in \mathcal{I_k}}\left(\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)\right) \right]\\
    &amp;= \frac{1}{n^2}  \sum_{i \in \mathcal{I_k}} \operatorname{Var}\left[ \left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right) \right] &amp;&amp;\text{iid} \\
    &amp;= \frac{|\mathcal{I_k}|}{n^2} \mathbb{E}\left[\left( \left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)\right)^2 \right]  \\
    &amp;=  \frac{|\mathcal{I_k}|}{n^2} \mathbb{E}\left[\mathbb{E}\left[\left( \left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)\right)^2 |X \right] \right]  \\
    &amp;=  \frac{|\mathcal{I_k}|}{n^2} \mathbb{E}\left[ \left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)^2\mathbb{E}\left[\left(1-\frac{T_{i}}{e\left(X_{i}\right)}\right)^2 |X \right] \right]  \\
    &amp;=  \frac{|\mathcal{I_k}|}{n^2} \mathbb{E}\left[\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)^2\frac{1}{e\left(X_{i}\right)^2}\mathbb{E}\left[ \left(e\left(X_{i}\right)-T_{i}\right)^2 |X \right] \right]  \\
    &amp;=  \frac{|\mathcal{I_k}|}{n^2} \mathbb{E}\left[\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)^2\frac{e\left(X_{i}\right)(1-e\left(X_{i}\right))}{e\left(X_{i}\right)^2} \right]  \\
    &amp;=  \frac{|\mathcal{I_k}|}{n^2} \mathbb{E}\left[\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)^2\left(\frac{1}{e\left(X_{i}\right)} -1\right) \right]  \\
    &amp;\leq  \frac{|\mathcal{I_k}|}{\eta n^2} \mathbb{E}\left[\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)^2 \right]  &amp;&amp; \text{Overlap} \\
    &amp;\leq  \frac{|\mathcal{I_k}|}{ n^2}o_{\mathbb{P}}(1)
\end{align*}\]</span></p>
<p>Therefore, because convergence on <span class="math inline">\(L^{2}\)</span>-norm provides convergence in probability (Chebyshev inequality), we have for <span class="math inline">\(k \in \{1, K\}\)</span>:</p>
<p><span class="math display">\[\sqrt{n}\, \frac{1}{n}  \sum_{i \in \mathcal{I_k}}\left(\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(1-\frac{T_i}{e\left(X_{i}\right)}\right)\right)  \stackrel{p}{\longrightarrow} 0\]</span></p>
<p>The second term can also controlled using similar arguments. Before detailed derivation, note that due to the uniform convergence of <span class="math inline">\(\hat e(.)\)</span> and the overlap assumption, there exist <span class="math inline">\(M\)</span> such that for all <span class="math inline">\(n &gt; M\)</span>, and for all <span class="math inline">\(X_i\)</span>,</p>
<p><span class="math display">\[ \frac{\eta}{2} \le \hat e(X_i) \le 1- \frac{\eta}{2}.\]</span></p>
<p>Therefore, there exist <span class="math inline">\(M\)</span> such that for all <span class="math inline">\(n &gt; M\)</span>, and for all <span class="math inline">\(X_i\)</span>, <span class="math display">\[\begin{align*}
    \frac{1}{\hat e(X)} - \frac{1}{e(X)} &amp;= \frac{e(X) - \hat e(X)}{\hat e(X) e(X)} \\
    &amp; \le 2\, \frac{e(X) - \hat e(X)}{\eta^2}.
\end{align*}\]</span></p>
<p>Derivations are very close to the ones for the first term, noting that, <span class="math display">\[\mathbb{E}\left[ \mathbb{E}\left[\frac{1}{n} \sum_{i \in \mathcal{I_k}} T_i\left(\left(Y_{i}-\mu_{1}\left(X_{i}\right)\right)\left(\frac{1}{\hat{e}^{\bar{\mathcal{I}_k}}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right)\right)\mid X_i \right]\right] =0,\]</span> so that,</p>
<p><span class="math display">\[\begin{align*}
\mathbb{E}\left[ \left(  \frac{1}{n} \sum_{i \in \mathcal{I_k}} T_i\left(Y_{i}-\mu_{1}\left(X_{i}\right)\right)\left(\frac{1}{\hat{e}^{\bar{\mathcal{I}_k}}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right)  \right)^2 \right]
&amp;= \operatorname{Var}\left[ \frac{1}{n} \sum_{i \in \mathcal{I_k}} T_i\left(Y_{i}-\mu_{1}\left(X_{i}\right)\right)\left(\frac{1}{\hat{e}^{\bar{\mathcal{I}_k}}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right) \right]\\
&amp;= \frac{1}{n^2} \sum_{i \in \mathcal{I_k}} \operatorname{Var}\left[ T_i\left(Y_{i}-\mu_{1}\left(X_{i}\right)\right)\left(\frac{1}{\hat{e}^{\bar{\mathcal{I}_k}}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right) \right] &amp;&amp; \text{iid}\\
&amp;= \frac{|\mathcal{I_k}|}{n^2} \mathbb{E}\left[ T\left(Y-\mu_{1}\left(X\right)\right)^2\left(\frac{1}{\hat{e}^{\bar{\mathcal{I}_k}}\left(X\right)}-\frac{1}{e\left(X\right)}\right)^2 \right] \\
&amp;\leq \frac{4|\mathcal{I_k}|}{\eta^4 n^2} \mathbb{E}\left[ T\left(Y-\mu_{1}\left(X\right)\right)^2\left(\hat{e}^{\bar{\mathcal{I}_k}}\left(X\right)-e\left(X\right)\right)^2 \right]\\
&amp;\leq \frac{4|\mathcal{I_k}|}{\eta^4 n^2} \mathbb{E}\left[ \left(Y-\mu_{1}\left(X\right)\right)^2\left(\hat{e}^{\bar{\mathcal{I}_k}}\left(X\right)-e\left(X\right)\right)^2 \right]&amp;&amp; \text{Sicne $T\leq 1$}\\
&amp;\leq \frac{4|\mathcal{I_k}|}{\eta^4 n^2} \mathbb{E}\left[\mathbb{E}\left[ \left(Y-\mu_{1}\left(X\right)\right)^2\left(\hat{e}^{\bar{\mathcal{I}_k}}\left(X\right)-e\left(X\right)\right)^2 | X \right]\right]\\
&amp;\leq \frac{4|\mathcal{I_k}|}{\eta^4 n^2} \mathbb{E}\left[ \mathbb{E}\left[\left(Y-\mu_{1}\left(X\right)\right)^2| X \right]\left(\hat{e}^{\bar{\mathcal{I}_k}}\left(X\right)-e\left(X\right)\right)^2 \right]\\
&amp;\leq \frac{4|\mathcal{I_k}|}{\eta^4 n^2} \mathbb{E}\left[ \operatorname{Var}\left[Y| X \right]\left(\hat{e}^{\bar{\mathcal{I}_k}}\left(X\right)-e\left(X\right)\right)^2 \right]\\
&amp;\leq \frac{4\operatorname{Var}\left[Y| X \right]|\mathcal{I_k}|}{\eta^4 n^2} \mathbb{E}\left[ \left(\hat{e}^{\bar{\mathcal{I}_k}}\left(X\right)-e\left(X\right)\right)^2 \right]\\
&amp;\leq \frac{4\operatorname{Var}\left[Y| X \right]|\mathcal{I_k}|}{\eta^4 n^2} o_{\mathbb{P}}(1)\\
\end{align*}\]</span></p>
<p>Therefore, for <span class="math inline">\(k \in \{1, K\}\)</span>:</p>
<p><span class="math display">\[\sqrt{n}\, \frac{1}{n} \sum_{i \in \mathcal{I_k}} T_i\left(Y_{i}-\mu_{1}\left(X_{i}\right)\right)\left(\frac{1}{\hat{e}^{\bar{\mathcal{I}_k}}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right)   \stackrel{p}{\longrightarrow} 0.\]</span></p>
<p>For the last term, the approach is different and will involve another assumption on the product of residuals,</p>
<p><span class="math display">\[\begin{align*}
    C_n^k &amp;= \sqrt{n}\frac{1}{n} \sum_{i \in \mathcal{I_k}}T_i\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)\left(\frac{1}{\hat{e}^{\bar{\mathcal{I}_k}}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right) \\
    &amp; \le  \sqrt{n}\sqrt{\frac{1}{n} \sum_{i \in \mathcal{I_k}}T_i\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)^2 } \sqrt{\frac{1}{n} \sum_{i \in \mathcal{I_k}} \left(\frac{1}{\hat{e}^{\bar{\mathcal{I}_k}}\left(X_{i}\right)}-\frac{1}{e\left(X_{i}\right)}\right)^2}  &amp;&amp; \text{C.S.} \\
    &amp;  \le \frac{\sqrt{n}}{ \eta} \sqrt{\frac{1}{n} \sum_{i \in \mathcal{I_k}}T_i\left(\hat \mu_1^{\bar{\mathcal{I}_k}}\left(X_{i}\right)-\mu_{1}\left(X_{i}\right)\right)^2 } \sqrt{\frac{1}{n} \sum_{i \in \mathcal{I_k}} \left(e(X_i) - \hat e^{\bar{\mathcal{I}_k}}(X_i)\right)^2  }  &amp;&amp; \text{Overlap} \\
    &amp; = \frac{\sqrt{n}}{ \eta}\, o_{\mathbb{P}}(\frac{1}{\sqrt{n}}) &amp;&amp; \text{Assumption} \\
    &amp; = \frac{1}{ \eta}\, o_{\mathbb{P}}(1)
\end{align*}\]</span></p>
<p>Each term <span class="math inline">\(A_n^k\)</span>, <span class="math inline">\(B_n^k\)</span>, and <span class="math inline">\(C_n^k\)</span> has been shown to be bounded by a term in <span class="math inline">\(o_{\mathbb{P}}(1)\)</span>. The remainder term with function <span class="math inline">\(\hat m^k_0(Y,A,X) - m_0(Y,A,X)\)</span> can also be controlled with the same derivation, except using the uniform convergence of <span class="math inline">\(\hat \mu^{\bar{\mathcal{I}_k}}_0(.)\)</span>. Since we have: <span class="math display">\[\sqrt{n}  (\hat \tau_{\text{AIPW}} - \hat\tau_{\text{AIPW}}^*) = \sum_{k=1}^K A_n^k + B_n^k + C_n^k \]</span> Therefore, <span class="math inline">\(\sqrt{n} (\hat \tau_{\text{AIPW}} - \hat\tau_{\text{AIPW}}^*) \stackrel{p}{\longrightarrow} 0\)</span>, so that <span class="math inline">\(\hat \tau_{\text{AIPW}}\)</span> has the same large sample properties as the oracle estimator.</p>
<p>To conclude,</p>
<p><span class="math display">\[\begin{equation*}
    \sqrt{n} (\hat \tau_{\text{AIPW}} - \tau) = \underbrace{\sqrt{n} (\hat \tau_{\text{AIPW}} - \hat\tau_{\text{AIPW}}^*)}_\textrm{$\stackrel{p}{\longrightarrow} 0$}  +  \underbrace{\sqrt{n}(\hat\tau_{\text{AIPW}}^* - \tau)}_\textrm{$\stackrel{d}{\rightarrow} \mathcal{N}\left(0, V_{\text{AIPW}}^* \right)$},
\end{equation*}\]</span></p>
<p>where <span class="math display">\[V_{\text{AIPW}}^* =\mathbb{E}\left[ \frac{\left(Y^{(1)}-\mu_1(X, V)\right)^2 }{e(X)} \right]+\mathbb{E}\left[ \frac{(Y^{(0)}-\mu_0(X, V))^2}{1-e(X)}  \right] +   \operatorname{Var}[\mu_1(X,V) - \mu_0(X,V)].\]</span></p>
</div></details>
</div>

</div>
