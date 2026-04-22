---
layout: post
title: "Chapter 3 — Randomized Controlled Trials"
date: 2023-10-03
excerpt: "Key assumptions and setup for randomized controlled trials: no interference, SUTVA, and randomization."
---

<div class="course-chapter">
<p class="chapter-nav">
  Course: <a href="/blog/">Finite Sample and Asymptotic Estimators in Causal Inference</a>
</p>

<p>To get two similar groups of people, the easiest way is to to randomize the treatment assignment. But first several assumptions on the population must be introduced.</p>
<div class="Assumption" id="Noinference" title="No Interference">
<p></p><details class="Assumption fbx-simplebox fbx-default" open=""><summary><strong>Assumption 3.1: </strong>No Interference</summary><div><span class="math display">\[  \forall i \in \mathcal{I}, \space Y_i(t_1, ..., t_i, ..., t_n) = Y_i(t_i) \]</span><p></p>
</div></details>
</div>
<p>This assumption means that the outcome is unaffected by anyone else’s treatment. Rather, the outcome for an individual <span class="math inline">\(i\)</span> is only a function of its own treatment. This assumption is not met when considering a vaccine as the treatment for example.</p>
<div class="Assumption" id="Consistency" title="Consistency">
<p></p><details class="Assumption fbx-simplebox fbx-default" open=""><summary><strong>Assumption 3.2: </strong>Consistency</summary><div><span class="math display">\[  \forall (t,i)\in  \{0,1\}\times \mathcal{I}, \space T = t \Rightarrow  Y_i = Y_i^{(t)} \]</span><p></p>
</div></details>
</div>
<p>For an individual <span class="math inline">\(i\)</span> if the treatment is <span class="math inline">\(T\)</span>, then the observed outcome <span class="math inline">\(Y\)</span> is the potential outcome under treatment <span class="math inline">\(T\)</span>. In other words, it means that all individuals who received <span class="math inline">\(T=t\)</span> actually received the exact same treatment (e.g. same dose). Note that this so-called consistency assumption has nothing to do with the consistency of an estimator.</p>
<p>When the treatment is binary <span class="math inline">\(T \in \{0,1\}\)</span> consistency and no interference translates to the stable unit treatment value assumption (<strong>SUTVA</strong>)</p>
<div class="Assumption" id="SUTVA" title="Stable Unit Treatment Value Assumption (SUTVA)">
<p></p><details class="Assumption fbx-simplebox fbx-default" open=""><summary><strong>Assumption 3.3: </strong>Stable Unit Treatment Value Assumption (SUTVA)</summary><div><span class="math display">\[ Y = T Y^{(1)} +(1-T)Y^{(0)}\]</span><p></p>
</div></details>
</div>
<p>Note that <span class="math inline">\(Y\)</span> is a random variable and that is corresponds to the observed outcome defined earlier.</p>
<p>As we just said the easiest way To get two similar groups of people is to use radomization in the treatement assignement. By this manipulation, the treatment is made independent of the potential outcome for each individual, which ensures what is called <strong>Exchangeability</strong>, <strong>ignorability</strong>, or <strong>internal validity</strong> of a trial. This assumption can also be written with mathematical terms:</p>
<div class="Assumption" id="Exchangeability" title="Exchangeability, ignorability">
<p></p><details class="Assumption fbx-simplebox fbx-default" open=""><summary><strong>Assumption 3.4: </strong>Exchangeability, ignorability</summary><div><span class="math display">\[ T\perp\mkern-9.5mu\perp (Y^{(0)}, Y^{(1)}) \]</span><p></p>
</div></details>
</div>
<p>In randomized controlled trials (RCTs) all these assumptions are verified and calculating the average treatment effect (ATE) is relatively straightforward due to the rigorous experimental design:</p>
<p><span class="math display">\[\begin{align*}
    \tau &amp;= \mathbb{E}[Y^{(1)} - Y^{(0)}]  \\
    &amp;= \mathbb{E}[Y^{(1)}|T = 1] - \mathbb{E}[Y^{(0)}|T = 0] &amp;&amp; \text{(Exchangeability)} \\
    &amp;= \mathbb{E}[Y|T = 1] - \mathbb{E}[Y|T = 0]  &amp;&amp; \text{(SUTVA)}
\end{align*}\]</span></p>
<p>Ignorability is mainly achieved using two designs of randomized controlled trials : Completely randomized trial and Bernoulli trial.</p>
<section class="level2" data-number="3.1" id="design">
<h2 class="anchored" data-anchor-id="design" data-number="3.1"> Design</h2>
</section>
<section class="level2" data-number="3.2" id="bernoulli-trial">
<h2 class="anchored" data-anchor-id="bernoulli-trial" data-number="3.2"> Bernoulli trial</h2>
<p>The so-called Bernoulli trial design is the simplest possible design. Assume you have at hand <span class="math inline">\(n\)</span> units, the treatment allocation follows a Bernoulli law with probability <span class="math inline">\(\pi\)</span> (for example <span class="math inline">\(\pi = 0.5\)</span>). The consequences is that the assignment mechanism is independent for all units. A disadvantage of such design is the fact that there is always a small probability that all units receive the treatment or no treatment. This is why other designs are possible, where the treatment allocation depends on previous decision for other units. The interest is to ensure to get a balanced group of treated and controls, and avoid a possible pathological case of high unbalance between the number of treated and control individuals.</p>
</section>
<section class="level2" data-number="3.3" id="completely-randomized-trial">
<h2 class="anchored" data-anchor-id="completely-randomized-trial" data-number="3.3"> Completely randomized trial</h2>
<p>The so-called completely randomized experiment considers a fixed number of subjects is assigned to receive the active treatment. The simplest completely randomized experiment takes an even number of units and divides them at random in two groups, with exactly one-half of the sample receiving the active treatment and the remaining units receiving the control treatment. This is accomplished, for example, by putting labels for the <span class="math inline">\(\mathrm{n}\)</span> units in an urn and drawing <span class="math inline">\(n_1 = n / 2\)</span> at random to be treated. Here, the probability of being treated for an individual is also constant for all units, namely <span class="math inline">\(n_1 / n\)</span>.</p>
<p>Since we have different kinds of designs for our study our random variables and their expectancy won’t behave the same way. Hence, we need to define new notations to understand what design we are talking about.</p>
<div class="Definition" id="expectancy-under-a-design" title="Expectancy under a Design">
<p></p><details class="Definition fbx-simplebox fbx-default" open=""><summary><strong>Definition 3.1: </strong>Expectancy under a Design</summary><div>We denote by <span class="math inline">\(\mathbb{E}_{\mathcal{B}}\)</span> (resp. <span class="math inline">\(\mathbb{E}_{\mathcal{C}}\)</span>) the expectancy of any random variables under a Bernoulli trial (resp. Completely randomized trial). We denote by <span class="math inline">\(\mathbb{Var}_{\mathcal{B}}\)</span> (resp. <span class="math inline">\(\mathbb{Var}_{\mathcal{C}}\)</span>) the variance of any random variables under a Bernoulli trial (resp. Completely randomized trial).<p></p>
</div></details>
</div>
<p>In both designs only the expectancy of the random variables that are not independent from <span class="math inline">\(T_i\)</span> will be affected. Hence, for instance if we are under a Completely randomized trial the random variables <span class="math inline">\(T_i\)</span> are not independent since the number of treated and untreated is fixed. <span class="math display">\[\begin{align*}
\mathbb{E}_{\mathcal{B}}[T] =  \mathbb{P}_{\mathcal{B}}[T=1] &amp;= \pi &amp;&amp; \text{def. of a Bernoulli trial}\\
\mathbb{E}_{\mathcal{C}}[T] =  \mathbb{P}_{\mathcal{B}}[T=1] &amp;= \frac{\left(\array{n-1\\n_1-1}\right)}{\left(\array{n\\n_1}\right)} &amp;&amp; \text{def. of a Completely randomized trial}\\
  &amp;= \frac{n_1}{n} \\
\end{align*}\]</span> Since the treatment are not I.I.D in a Completely randomized trial we have: <span class="math display">\[\begin{align*}
\underbrace{\mathbb{E}_{\mathcal{B}}[TT^{'}]}_{\pi^2} &amp;\neq \mathbb{E}_{\mathcal{C}}[TT^{'}]
\end{align*}\]</span> However, using Exchangeability we have for <span class="math inline">\(t \in \{0, 1\}\)</span>: <span class="math display">\[\begin{align*}
\mathbb{E}_{\mathcal{B}}[Y^{(t)}] &amp;= \mathbb{E}_{\mathcal{C}}[Y^{(t)}]
\end{align*}\]</span> And this implies that the value of the ATE does change with the disgn.</p>
<p>Now that we have presented all the framework in the case of RCTs. We can introduce our first estimator for the Average Treatment Effect.</p>
</section>

</div>
