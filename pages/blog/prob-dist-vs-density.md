<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.css" integrity="sha384-yFRtMMDnQtDRO8rLpMIKrtPCD5jdktao2TV19YiZYWMDkUR5GQZR/NOVTdquEx1j" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.js" integrity="sha384-9Nhn55MVVN0/4OFx7EE5kpFBPsEMZxKTCnA+4fqDmg12eCTqGi6+BB2LjY8brQxJ" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>


Some time ago, my doctoral advisor, [Mikael Skoglund](https://people.kth.se/~skoglund/), pointed to me I was referring to the _probability density function_ of a random variable as _distribution_, and that it was wrong. I was a bit puzzled, since I learned the definitions of these concepts during the bachelor's degree. However, after reading machine learning papers, these definitions blurred in my mind, since in many papers the two are confused with each other and/or used indistinctibly. In fact, even I propagated this misconception.

Recently, while reviewing the documents from some master's students, I realized that this has become a common misconception. For this reason, I decided to write about (i) the differences between these terms and (ii) how to write about them more precisely in academic texts.

## What is the difference between the distribution and the density of a random variable?

### Random variables and the probability distribution

In order to answer this question we need first to define what a *random variable* is:

---
**Random variable:** *Let $(\Omega, \mathcal{F}, \mathbb{P})$ be a probability space. Then, a random variable $X: \Omega \rightarrow \mathcal{X}$ is a real-valued function from the set of outcomes $\Omega$ to the target space $\mathcal{X} \subseteq \mathbb{R}$. This function must satisfy that all outcomes $\omega$ that can generate instances $X(\omega)$ from a Borel set $B$ belong to the $\sigma$-algebra $\mathcal{F}$ (or the set of events), for all Borel sets of $\mathcal{X}$, $\mathcal{B}(\mathcal{X})$; that is, $\lbrace \omega: X(\omega) \in B\rbrace \in \mathcal{F}$ for each Borel set $B \in \mathcal{B}(\mathcal{X})$.*

---

We are usually interested in the probability that a value of a random variable $X$ belongs to a set $B$. For example, the probability that $X = 7$ or $X > 3$, for which the set $B$ is $\lbrace{7}\rbrace$ and $\lbrace x : x > 3, x \in \mathcal{X} \rbrace$, respectively. Formally, this is the probabiliy of the set of outcomes for which the random variable $X$ yields values from $B$, i.e., $\mathbb{P}(\lbrace \omega: X(\omega) \in B\rbrace)$. For simplicity, however, we write $\mathbb{P}(X \in B)$ instead. The *probability distribution* is the set function that tells us this probability. 

---
**Probability distribution:** *Let $X$ be a random variable on the probability space $(\Omega, \mathcal{F}, \mathbb{P})$. The probability distribution $P_X: \mathcal{B}(\mathcal{X}) \rightarrow [0,1]$ of the random variable $X$ is the set function on $\mathcal{B}(\mathcal{X})$ defined by $P_X(B) = \mathbb{P}(X \in B)$.*

---

Note that, once the probability distribution $P_X$ is defined, we can construct another probability space, namely $(\mathcal{X},\mathcal{B}(\mathcal{X}),P_X)$. In this space, the outcomes of a random variable $X$ are now $x \in \mathcal{X}$, the events are sets of such outcomes $B \in \mathcal{B}(\mathcal{X})$, and the probability of such events is measured as $P_X(B)$. If we construct this probability space, then the original sets of outcomes $\Omega$ and events $\mathcal{F}$ can remain as abstract concepts.

### Discrete random variables and the probability mass function

We define a *discrete random variable* as follows:

---
**Discrete random variable**: *We say a random variable $X$ is discrete if there is a countable set $K$ such that $P_X(K) = 1$. For such a random variable, we write $K = \lbrace x_k \rbrace_k$. Then, the probability distribution of $X$ is given by $P_X = \sum_k p_k \delta[x_k]$, where $p_k = \mathbb{P}(X=x_k)$ and $\delta[\cdot]$ is the Kronecker delta.*

**Probability mass function (pmf)**: *Let us consider a discrete random variable $X$. The probability mass function (pmf) $p_X: \mathcal{X} \rightarrow [0,1]$ is defined as $p_X(x) = \mathbb{P}(X=x)$.*

---

Note that if we consider a Borel set $B= \lbrace x \rbrace$ such that $x \in \mathcal{X}$, then there is an equivalence between the pmf and the probability distribution, namely, $p_X(x) = P_X(\lbrace x \rbrace)$. Therefore, the pmf $p_X(x)$ tells us the probabiliy of the random variable $X$ taking the value $x$.

---
**Example**: Imagine the setting of the rolling of two dice. Then, we consider the probability space $(\Omega, \mathcal{F}, \mathbb{P})$, where the set of outcomes is the possible outcomes of the dice $\Omega = \lbrace (i,j): i,j=1,2,...,6 \rbrace$, the $\sigma$-algebra is the power set of $\Omega$, $\mathcal{P}(\Omega)$ (or the set of all possible events), and the probabiliy measure is $\mathbb{P} = \frac{1}{36}\gamma$, where $\gamma$ is the counting measure. We consider the random variable $X$ to be the sum of the two dice outcomes.

* If we want to know the probability that $X$ takes the value $7$, we can either look at the distribution of the set $\lbrace 7 \rbrace$ or at the pmf evaluated at 7. That is, $\mathbb{P}(X = 7) = P_X(\lbrace 7 \rbrace) = p_X(7) = \frac{1}{6}$.
* However, if we consider the Borel set $B = \lbrace 2,4,5 \rbrace$, the probability that $X$ takes any of the values from this set is $\mathbb{P}(X \in B) = P_X(B) = \frac{1}{36}(\gamma(X = 2) + \gamma(X=4) + \gamma(X=5)) = \frac{2}{9}$. 

---

### Absolutely continuous random variables and the probability density function 

We define an *absolutely continuous random variable* as follows:

---
**Absolutely continuous random variable**: *We say a random variable $X$ is absolutely continuous if it exists a non-negative Borel measurable function $f_X$ such that $P_X(B) = \int_B f_X(x) dx$ for all $B \in \mathcal{B}(\mathcal{X})$.*

**Probability density function (pmf)**: *Let us consider an absolutely continuous random variable $X$. Then, the non-negative Borel measurable function $f_X: \mathcal{X} \rightarrow \mathbb{R}^+$ is the probabiliy density function of $X$.*

---

Therefore, the probabiliy that $X$ takes any of the values of a Borel set $B$ is the probability distribution evaluated at $B$, i.e., $\mathbb{P}(X \in B) = P_X(B)$, but the integral of the pdf over all the elements $x$ from $B$, i.e., $\mathbb{P}(X \in B) = \int_B f_X(x) dx$. 

In other words, the value of the probability distribution $P_X(B)$ tells us the probabiliy of $X$ belonging to a particular set $B$, while the value of the pdf $f_X(x)$ tells us (_informally_) the probability of $X$ belonging to the infinitessimal interval $\left(x-\frac{\epsilon}{2},x+\frac{\epsilon}{2}\right)$, where $\epsilon \rightarrow 0$. Hence,

* $P_X(\lbrace x \rbrace) = 0$ for all $x \in \mathcal{X}$, while $f_X(x) > 0$ for some $x \in \mathcal{X}$. For example, if we consider a Gaussian random variable with mean $\mu$ and variance $\sigma^2 = 0.1$, then the distribution value of $\lbrace \mu \rbrace$ is $P_X(\lbrace \mu \rbrace) = 0$, while the pdf at that point is $f_X(\mu) \approx 1.26$. This is because the probability is highly concentrated around the mean (it has high _density_), however, the probability of _exactly_ the mean is 0.

## How can we be precise when talking about them?

The simplest way to write effectively about these concepts is using the exact definitions above :). There is no need to use the exact same notation I used, but to make sure the disambiguation between the terms is clear and that they are properly defined.

However, in many machine learning papers, the only notions that are used are the _probability density function_ (pdf) and the _probability mass function_ (pmf). I realize that the preferred notation is $p(x)$ for either $p_X(x)$ or $f_X(x)$. If this is the case, I recommend using the following:

* Somewhere in the text (preferrably in a potential *Notation* section) write something on the lines of: "*We write $p(X)$ and say density of $X$ to refer to the probability density function (pdf) or the probability mass function (pmf) of the random variable $X$, depending if it is continuous or discrete, respectively. Moreover, we write $p(x)$ instead of $p(X=x)$ for brevity.*"

* Then, instead of writing something like "*We learn the distribution $q_{\phi}(Y \vert X)$ ...*" you can write some of the following:

  * "*We learn the distribution described by the density $q_{\phi}(Y \vert X)$.*"
  * "*We learn the distribution described by $q_{\phi}(Y \vert X)$.*"
  * "*We learn the density $q_{\phi}(Y \vert X)$.*"

## And that is all

Well, that is the end of this (and my first) blog. Thank you very much for reading until the end and I hope I did not bore you too much or I did not write too much incoherences. 

Please, let me know if you have any suggestions.

P.D.: If this blog did not shed any light in the differences between the two notions I recommend the following book, they explain things much better than I do.

* McDonald, John N., and Neil A. Weiss. _A course in real analysis._ Taylor & Francis US, 1999.
