---
layout: post
title: "Chapter 1 — Statistical Introduction"
date: 2023-10-01
excerpt: "Definitions of statistical models, estimators, and asymptotic theory — the mathematical foundations for causal inference."
---

<div class="course-chapter">
<p class="chapter-nav">
  Course: <a href="/blog/">Finite Sample and Asymptotic Estimators in Causal Inference</a>
</p>

<section class="level2" data-number="1.1" id="statistical-models">
<h2 class="anchored" data-anchor-id="statistical-models" data-number="1.1"> Statistical models</h2>
<div class="Definition" id="statistical-model" title="Statistical model">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.1: </strong>Statistical model</summary><div>A statistical model <span class="math inline">\(\mathcal{M}\)</span> is the association of:<p></p>
<ul>
<li>a state space <span class="math inline">\(\mathcal{X}\)</span></li>
<li>a family of probabilities <span class="math inline">\(\mathcal{C}\)</span> on <span class="math inline">\((\mathcal{X}, \mathcal{T}(\mathcal{X}))\)</span></li>
</ul>
<p>With <span class="math inline">\(\mathcal{T}(\mathcal{X})\)</span> is the <span class="math inline">\(\sigma\)</span>-field induced by <span class="math inline">\(\mathcal{X}\)</span>. We say that a model <span class="math inline">\(\mathcal{M} = (\mathcal{X}, \mathcal{C})\)</span> is parametric if <span class="math inline">\(\mathcal{C}\)</span> corresponds to a family of probabilities <span class="math inline">\(\{\mathbb{P}_\theta, \theta \in \Theta\}\)</span>, where <span class="math inline">\(\Theta\)</span> is a sub-set of <span class="math inline">\(\mathbb{R}^d\)</span> with <span class="math inline">\(d\geq1\)</span>; there exists a function mapping for each <span class="math inline">\(\theta\)</span> an element <span class="math inline">\(\mathbb{P}_\theta \in \mathcal{C}\)</span>.</p>
<p>The model is identifiable if the mapping function is injective, if <span class="math inline">\(\mathbb{P}_\theta = \mathbb{P}_{\theta'}\Rightarrow \theta = \theta'\)</span>.</p>
</div></details>
</div>
<p>In other words, <span class="math inline">\(\mathcal{X}\)</span> is the space in which the data, namely the observed random variables take their values. For instance, if we want to study whether a coin is balanced or not, we can set <span class="math inline">\(\mathcal{X} =\{0,1\}\)</span> (0 for heads and 1 for tails) and <span class="math inline">\(\mathcal{C} = \{\mathbb{P}_{\theta}, \theta \in [0,1]\}\)</span> where <span class="math inline">\(\mathbb{P}_\theta\)</span> is the Bernoulli distribution of parameter <span class="math inline">\(\theta\)</span>.</p>
<div class="Definition" id="statistic" title="Statistic">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.2: </strong>Statistic</summary><div>Let <span class="math inline">\(\mathcal{M} = (\mathcal{X}, \mathcal{C})\)</span> be a statistical model and <span class="math inline">\((\mathcal{Z}, \mathcal{T}(\mathcal{Z}))\)</span> a measurable space. We define a statistic <span class="math inline">\(\mathsf{S}\)</span> on the model <span class="math inline">\(\mathcal{M}\)</span> as a measurable function of <span class="math inline">\((\mathcal{X}, \mathcal{T}(\mathcal{X}))\)</span> to <span class="math inline">\((\mathcal{Z}, \mathcal{T}(\mathcal{Z}))\)</span>.<p></p>
</div></details>
</div>
<div class="Definition" id="n-sample" title="n-sample">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.3: </strong><span class="math inline">\(n\)</span>-sample</summary><div>Let <span class="math inline">\(\mathcal{M} = (\mathcal{X}, \mathcal{C})\)</span> be a statistical model and <span class="math inline">\(n \in \mathbb{N}^*\)</span>. We say that <span class="math inline">\((X_1, ....., X_n)\)</span> is a <span class="math inline">\(n\)</span>-sample of <span class="math inline">\(\mathcal{M}\)</span> if <span class="math inline">\((X_1, ....., X_n)\)</span> are n independent and identically distributed random variables from <span class="math inline">\(\mathbb{Q} \in \mathcal{C}\)</span><p></p>
</div></details>
</div>
</section>
<section class="level2" data-number="1.2" id="estimators">
<h2 class="anchored" data-anchor-id="estimators" data-number="1.2"> Estimators</h2>
<div class="Definition" id="estimator" title="Estimator">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.4: </strong>Estimator</summary><div>Let <span class="math inline">\(\mathcal{M} = (\mathcal{X}, \{\mathbb{P}_\theta, \theta \in \Theta\})\)</span> be a parametric statistical model and <span class="math inline">\(g : \Theta \mapsto \mathbb{R}^q\)</span> a function. An estimator <span class="math inline">\(\mathsf{T}\)</span> of <span class="math inline">\(g(\theta)\)</span> is a statistic in <span class="math inline">\(\mathbb{R}^q\)</span>.<p></p>
</div></details>
</div>
<section class="level3" data-number="1.2.1" id="bias-and-variance-of-an-estimator">
<h3 class="anchored" data-anchor-id="bias-and-variance-of-an-estimator" data-number="1.2.1"> Bias and Variance of an estimator</h3>
<div class="Definition" id="bias-of-an-estimator" title="Bias of an estimator">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.5: </strong>Bias of an estimator</summary><div>Let <span class="math inline">\(\mathcal{M} = (\mathcal{X}, \{\mathbb{P}_\theta, \theta \in \Theta\})\)</span> be a parametric statistical model, <span class="math inline">\(g: \Theta\rightarrow \mathbb{R}^q\)</span> a measurable function and <span class="math inline">\(\mathsf{T}\)</span> an estimator of the function <span class="math inline">\(g: \Theta\mapsto g(\theta)\)</span>. The bias of the estimator <span class="math inline">\(\mathsf{T}\)</span> is defined as: <span class="math display">\[ b_g(\theta, \mathsf{T}) = \mathbb{E}_\theta[T] - g(\theta)\]</span> We say that <span class="math inline">\(\mathsf{T}\)</span> is an unbiased estimator of the function <span class="math inline">\(g: \Theta\mapsto g(\theta)\)</span> if: <span class="math display">\[\forall \theta \in \Theta \quad \mathbb{E}_\theta[T] = g(\theta)\]</span><p></p>
</div></details>
</div>
<p>If we take back the previous example, let <span class="math inline">\((X_1, ....., X_n)\)</span> be an <span class="math inline">\(n\)</span>-sample of the statistical model <span class="math inline">\(\mathcal{M} = (\mathcal{X}, \{\mathbb{P}_\theta, \theta \in \Theta\})\)</span> where <span class="math inline">\(\mathcal{X} =\{0,1\}\)</span> and <span class="math inline">\(\mathbb{P}_\theta\)</span> is the Bernoulli distribution of parameter <span class="math inline">\(\theta\)</span>. We define <span class="math inline">\(\bar{X}_n\)</span> as the empirical mean then have:</p>
<p><span class="math display">\[\begin{align*}
    \mathrm{E}[\bar{X}_n] &amp;= \mathbb{E}\left[\frac{1}{n} \sum_{i=1}^{n} X_i\right] \\
    &amp;= \frac{1}{n} \sum_{i=1}^{n} \mathbb{E}[X_{i}] &amp;&amp; \text{linearity of $\mathbb{E}[.]$}\\
    &amp;= \frac{1}{n} \sum_{i=1}^{n} \theta &amp;&amp; \text{i.i.d according to $\mathbb{P}_\theta$} \\
    &amp;= \frac{1}{n} \, n \, \theta\\
    &amp;= \theta
\end{align*}\]</span></p>
<p>Therefore the empirical mean is an unbiased estimator of the function <span class="math inline">\(g:\theta \mapsto \theta\)</span>. Could we find another unbiased estimator of the average? Of course, in fact the estimator taking the <span class="math inline">\(k^{th}\)</span> value of the sample is also an unbiased estimator of <span class="math inline">\(\theta\)</span>. However, it will suffer of what we will call a high variance.</p>
<div class="Definition" id="variance-of-an-estimator" title="Variance of an estimator">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.6: </strong>Variance of an estimator</summary><div>Let <span class="math inline">\(\mathcal{M} = (\mathcal{X}, \{\mathbb{P}_\theta, \theta \in \Theta\})\)</span> be a parametric statistical model, <span class="math inline">\(g: \Theta\rightarrow \mathbb{R}^q\)</span> a measurable function and <span class="math inline">\(\mathsf{T}\)</span> an estimator of the function <span class="math inline">\(g: \Theta\mapsto g(\theta)\)</span>. The variance of the estimator <span class="math inline">\(\mathsf{T}\)</span> is defined as: <span class="math display">\[\operatorname{Var}_\theta(\mathsf{T}) = \mathbb{E}_\theta[(T - \mathbb{E}_\theta[T])^2]\]</span><p></p>
</div></details>
</div>
<p>Beyond bias, a very important property is how estimates spread around the average value. For example, between two unbiased estimators, a way to choose a better one would be the one being the more precise; that is with the smaller variance. Again if we illustrate this with the coin example we have:</p>
<p><span class="math display">\[\begin{align*}
    \operatorname{Var}\left[\bar{X}_n\right] &amp;=  \operatorname{Var}\left[\frac{1}{n} \sum_{i=1}^{n} X_{i}\right] \\
    &amp;= \frac{1}{n^2} \operatorname{Var}\left[ \sum_{i=1}^{n} X_{i}\right] &amp;&amp; \text{properties of variance} \\
    &amp;= \frac{1}{n^2} n\,\operatorname{Var}\left[  X\right] &amp;&amp; \text{independent observations} \\
    &amp;= \frac{\operatorname{Var}\left[X \right]}{n}.
\end{align*}\]</span></p>
<p>This formula illustrates that the properties of the estimator in this case depends on both the underlying distribution and the sample size. In particular, we see that the more value we use in our estimator the smaller its variance is and therefore the more precise our estimator is.</p>
</section>
</section>
<section class="level2" data-number="1.3" id="large-sample-properties">
<h2 class="anchored" data-anchor-id="large-sample-properties" data-number="1.3"> Large sample properties</h2>
<p>These properties characterize estimators when the size of the <span class="math inline">\(n\)</span>-sample gets large, and are also called asymptotic properties. A very famous property is called consistency, when it holds it ensures that the probability to find an estimator <span class="math inline">\(\mathsf{T}\)</span> close to its estimand is getting bigger with <span class="math inline">\(n\)</span>.</p>
<div class="Definition" id="Consistency" title="Consistency">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.7: </strong>Consistency</summary><div>Let <span class="math inline">\(\mathcal{M}_n = (\mathcal{X}_{n}, \{\mathbb{P}_{n,\theta}, \theta \in \Theta\})\)</span> sequence of parametric statistical model, <span class="math inline">\(g: \Theta\rightarrow \mathbb{R}^q\)</span> a measurable function. Let <span class="math inline">\(\{\mathsf{T}_n | n \in \mathbb{N}^* \}\)</span> be a sequence of estimators of <span class="math inline">\(g: \Theta\mapsto g(\theta)\)</span>, we say that <span class="math inline">\(\mathsf{T}_n\)</span> is a consistent estimator if: <span class="math display">\[\forall \epsilon &gt; 0 \quad \forall \theta \in \Theta \quad \lim_{n \rightarrow \infty} \mathbb{P}\left(\left|\mathsf{T}_n-g(\theta)\right|&gt;\varepsilon\right) = 0\]</span><p></p>
</div></details>
</div>
<p>Note that this can be linked to <span class="math inline">\(L^2\)</span> convergence of random variables. Hence a sufficient condition to achieve Consistency [<a href="Finte-sample-and-asymptotic-estimators-properties-in-Causal-Inference.epub#Consistency">2</a>] is <span class="math inline">\(L^2\)</span> convergence:</p>
<div class="Proposition" id="sufficient-condition-ta-achieve-consistency" title="Sufficient condition ta achieve consistency">
<p></p><details class="Proposition fbx-simplebox fbx-default" open=""><summary><strong>Proposition 1.1: </strong>Sufficient condition ta achieve consistency</summary><div>Let <span class="math inline">\(\{\mathsf{T}_n | n \in \mathbb{N}^* \}\)</span> be a sequence of estimators of <span class="math inline">\(g: \Theta\mapsto g(\theta)\)</span> such that: <span class="math display">\[\begin{equation*}
    \lim_{n \rightarrow \infty} \mathbb{E}\left[\left(\mathsf{T}_n-g(\theta)\right)^{2}\right] = 0
\end{equation*}\]</span><p></p>
<p>Then <span class="math inline">\(\mathsf{T}_n\)</span> is a consistent estimator of <span class="math inline">\(g(\theta)\)</span>.</p>
</div></details>
</div>
<div class="Proof unnumbered" id="Proof*-1.1">
<p></p><details class="Proof fbx-simplebox fbx-default"><summary><strong>Proof</strong></summary><div>this is a direct consequence of Chebyshev’s inequality to have,<p></p>
<p><span class="math display">\[\begin{equation*}
    \mathbb{P}\left(\left|\widehat{\theta}-\theta\right| \geq \varepsilon\right) \leq \frac{\mathbb{E}\left[\left(\hat{\theta}-\theta\right)^{2}\right]}{\varepsilon^{2}}.
\end{equation*}\]</span></p>
</div></details>
</div>
<p>This property means that the distribution of <span class="math inline">\(\mathsf{T}_n\)</span> concentrates around <span class="math inline">\(g(\theta)\)</span> as <span class="math inline">\(n\)</span> gets bigger. We also say that <span class="math inline">\(\mathsf{T}_n\)</span> is converging in law toward <span class="math inline">\(g(\theta)\)</span>. Note that unlike unbiasedness which state an estimator’s property of any sample size, here the property characterize the distribution if <span class="math inline">\(n\)</span> is sufficiently large. If an estimator is not consistent, there is little interest - if no interest - to gather a lot of data.</p>
<p>Again if we illustrate this with the coin flip example, we have the consistency of the empirical mean estimator using the strong law of numbers.</p>
<p>Now we define mathematically the fact that an estimator’s distribution clusters around a target parameter, it says nothing about how it does it. It can be done with different rates and shapes. Therefore, we define below how we can understand a rate of convergence.</p>
<div class="Definition" id="Rate_of_convergence" title="Rate of convergence">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.8: </strong>Rate of convergence</summary><div>Let <span class="math inline">\(\mathcal{M}_n = (\mathcal{X}_{n}, \{\mathbb{P}_{n,\theta}, \theta \in \Theta\})\)</span> sequence of parametric statistical model, <span class="math inline">\(g: \Theta\rightarrow \mathbb{R}^q\)</span> a measurable function. Let <span class="math inline">\(\{\mathsf{T}_n | n \in \mathbb{N}^* \}\)</span> be a sequence of estimators of <span class="math inline">\(g: \Theta\mapsto g(\theta)\)</span> and <span class="math inline">\(\{r_n | n \in \mathbb{N}^* \}\)</span> a sequence that converges to infinity, we say that <span class="math inline">\(\mathsf{T}_n\)</span> has rate of convergence <span class="math inline">\(r_{n}\)</span> if: <span class="math display">\[\forall \epsilon &gt; 0 \quad \forall \theta \in \Theta \quad \lim_{n \rightarrow \infty} \mathbb{P}\left(\left|r_n(\mathsf{T}_n-g(\theta))\right|&gt;\varepsilon\right) = 0\]</span><p></p>
</div></details>
</div>
<p>The rate <span class="math inline">\(r_n\)</span> tells us how fast our estimator clusters around its estimand. This is very important, because the higher <span class="math inline">\(r_n\)</span> the higher we can get information with a restricted set of data. Usually we can hear about <span class="math inline">\(\sqrt{n}\)</span> consistent estimator.</p>
<p>Another property we would like to have – beyond the rate – is the shape of the asymptotic distribution. It means that we can characterize not only the speed, but we know that <span class="math inline">\(\mathsf{T}_n\)</span> is clustering around <span class="math inline">\(g(\theta)\)</span>. A very famous property is the asymptotic normality, that is the clustering is homogeneous around the target parameter.</p>
<div class="Definition" id="Asymptotic_normality" title="Asymptotic normality">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 1.9: </strong>Asymptotic normality</summary><div>Let <span class="math inline">\(\mathcal{M}_n = (\mathcal{X}_{n}, \{\mathbb{P}_{n,\theta}, \theta \in \Theta\})\)</span> sequence of parametric statistical model, <span class="math inline">\(g: \Theta\rightarrow \mathbb{R}^q\)</span> a measurable function. Let <span class="math inline">\(\{\mathsf{T}_n | n \in \mathbb{N}^* \}\)</span> be a sequence of estimators of <span class="math inline">\(g: \Theta\mapsto g(\theta)\)</span>, we say that <span class="math inline">\(\mathsf{T}_n\)</span> is said to have an asymptotic standard normal distribution if: <span class="math display">\[\forall \theta \in \Theta \quad  \sqrt{n}(\mathsf{T}_n-g(\theta))\stackrel{\mathbb{P}_\theta}{\longrightarrow } \mathcal{N}(0, \Gamma(\theta))\]</span> Where for all <span class="math inline">\(\theta \in \Theta\)</span>, <span class="math inline">\(\Gamma(\theta)\)</span> is a symmetrical and positive matrix.<p></p>
</div></details>
</div>
<p>Usually <span class="math inline">\(\sqrt{n}\)</span> consistency and asymptotically normality is the best we can do.</p>
</section>

</div>
